{
  "name": "aviator-tracker-app",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Aviator Tracker App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import "./index.css";

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
import { useState } from "react";

export default function App() {
  const [input, setInput] = useState("");
  const [multipliers, setMultipliers] = useState([]);
  const [signals, setSignals] = useState([]);

  const addMultiplier = () => {
    const value = parseFloat(input);
    if (!isNaN(value)) {
      const newList = [...multipliers, value];
      setMultipliers(newList);
      if (value > 5) {
        setSignals([...signals, `🔥 ${value} detected! Signal!`]);
      }
    }
    setInput("");
  };

  return (
    <div className="min-h-screen bg-black text-white p-4">
      <h1 className="text-2xl font-bold mb-4 text-center">🛫 Aviator Tracker App</h1>

      <div className="flex gap-2 mb-4 justify-center">
        <input
          type="number"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          className="p-2 rounded bg-gray-800 border border-gray-700"
          placeholder="Enter multiplier"
        />
        <button onClick={addMultiplier} className="bg-green-600 px-4 py-2 rounded hover:bg-green-700">
          Add
        </button>
      </div>

      <div className="mb-4">
        <h2 className="text-xl mb-2">📜 History</h2>
        <ul className="space-y-1">
          {multipliers.map((m, i) => (
            <li key={i} className="text-sm">
              Round {i + 1}: {m}
            </li>
          ))}
        </ul>
      </div>

      <div>
        <h2 className="text-xl mb-2">⚠️ Signals</h2>
        <ul className="space-y-1 text-green-400">
          {signals.map((s, i) => (
            <li key={i} className="text-sm">
              {s}
            </li>
          ))}
        </ul>
      </div>
    </div>
  );
}
body {
  margin: 0;
  font-family: Arial, sans-serif;
}
