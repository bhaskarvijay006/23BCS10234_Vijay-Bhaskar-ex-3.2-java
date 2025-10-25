# 23BCS10234_Vijay-Bhaskar-ex-3.2-java

import React, { useState } from "react";
import { motion } from "framer-motion";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";

export default function LibraryUI() {
  const [books, setBooks] = useState([
    { id: 1, title: "Atomic Habits" },
    { id: 2, title: "Clean Code" },
    { id: 3, title: "The Pragmatic Programmer" },
  ]);

  const [query, setQuery] = useState("");
  const [newBook, setNewBook] = useState("");

  const filteredBooks = books.filter((b) =>
    b.title.toLowerCase().includes(query.toLowerCase())
  );

  function handleAdd() {
    if (!newBook.trim()) return;
    setBooks([
      ...books,
      { id: Date.now(), title: newBook.trim() }
    ]);
    setNewBook("");
  }

  function handleRemove(id) {
    setBooks(books.filter((b) => b.id !== id));
  }

  return (
    <div className="max-w-lg mx-auto p-6 grid gap-6">
      <h1 className="text-2xl font-bold text-center">Library Manager 📚</h1>

      {/* Search */}
      <Input
        placeholder="Search book by title..."
        value={query}
        onChange={(e) => setQuery(e.target.value)}
      />

      {/* Add Book */}
      <div className="flex gap-2">
        <Input
          placeholder="New book title"
          value={newBook}
          onChange={(e) => setNewBook(e.target.value)}
        />
        <Button onClick={handleAdd}>Add</Button>
      </div>

      {/* Book List */}
      <div className="grid gap-3">
        {filteredBooks.length === 0 ? (
          <p className="text-center text-slate-500">No books found</p>
        ) : (
          filteredBooks.map((b) => (
            <motion.div
              key={b.id}
              initial={{ opacity: 0, y: 8 }}
              animate={{ opacity: 1, y: 0 }}
            >
              <Card className="flex justify-between items-center px-4 py-3">
                <CardContent className="p-0 font-medium">{b.title}</CardContent>
                <Button size="sm" variant="destructive" onClick={() => handleRemove(b.id)}>
                  Remove
                </Button>
              </Card>
            </motion.div>
          ))
        )}
      </div>
    </div>
  );
}
