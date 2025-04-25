AGENTES IA OPTIMIZADOS
import React, { useState } from "react";
import { Button } from "@/components/ui/button";

export default function HackerIAInterface() {
  const [prompt, setPrompt] = useState("");
  const [response, setResponse] = useState("");

  const handleSubmit = async () => {
    const res = await fetch("/api/generate", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ prompt }),
    });
    const data = await res.json();
    setResponse(data.result);
  };

  return (
    <div className="min-h-screen bg-black text-green-400 font-mono p-4">
      <h1 className="text-2xl mb-4">🧠 Terminal IA - Estilo Hacker</h1>
      <div className="mb-4">
        <label className="block mb-1">Ingresa tu prompt:</label>
        <textarea
          value={prompt}
          onChange={(e) => setPrompt(e.target.value)}
          className="w-full p-2 bg-black border border-green-500 text-green-300"
          rows={5}
        />
      </div>
      <Button onClick={handleSubmit} className="bg-green-600 hover:bg-green-700">
        Ejecutar Agente IA
      </Button>
      <div className="mt-6 p-4 border border-green-500 bg-black">
        <h2 className="text-xl mb-2">📡 Respuesta:</h2>
        <pre>{response}</pre>
      </div>
    </div>
  );
}
