import { useState, useEffect } from "react";
import { Card, CardContent } from "./components/ui/card";
import { Input } from "./components/ui/input";
import { Button } from "./components/ui/button";
import { Search, DollarSign } from "lucide-react";

const swordData = [
  { name: "Shadow Blade", value: "3,500 Coins", rarity: "Legendary" },
  { name: "Inferno Katana", value: "2,000 Coins", rarity: "Epic" },
  { name: "Aqua Saber", value: "1,200 Coins", rarity: "Rare" }
];

export default function BladeBallTrading() {
  const [search, setSearch] = useState("");
  const [mouseX, setMouseX] = useState(0);
  const [mouseY, setMouseY] = useState(0);

  useEffect(() => {
    const handleMouseMove = (e) => {
      setMouseX(e.clientX / window.innerWidth - 0.5);
      setMouseY(e.clientY / window.innerHeight - 0.5);
    };
    window.addEventListener("mousemove", handleMouseMove);
    return () => window.removeEventListener("mousemove", handleMouseMove);
  }, []);

  const filteredSwords = swordData.filter((sword) =>
    sword.name.toLowerCase().includes(search.toLowerCase())
  );

  return (
    <div
      className="min-h-screen flex flex-col items-center justify-center bg-gradient-to-b from-blue-600 to-black text-white space-y-8"
      style={{
        transform: `translate(${mouseX * 10}px, ${mouseY * 10}px)`,
        transition: "transform 0.1s ease-out"
      }}
    >
      <div className="flex justify-center mb-6">
        <img src="/Blade_Ball_2023.webp" alt="Blade Ball" className="w-full max-w-xs md:max-w-md lg:max-w-lg" />
      </div>
      <h1 className="text-5xl font-extrabold text-center mb-6">Blade Ball Trading Values</h1>
      <div className="flex gap-4 justify-center mb-8 w-full max-w-xl relative">
        <Input
          placeholder="Search for a sword..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="bg-gray-800 text-white border-gray-500 px-4 py-3 w-full text-lg rounded-md pr-14 transition-transform duration-300 hover:scale-105"
        />
        <Button variant="outline" className="absolute right-2 top-1/2 transform -translate-y-1/2 border-gray-500 text-white px-4 py-3 transition-transform duration-300 hover:scale-110">
          <Search className="w-6 h-6" />
        </Button>
      </div>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {filteredSwords.map((sword, index) => (
          <Card key={index} className="bg-gray-900 text-white border-gray-700 transition-transform duration-300 hover:scale-105">
            <CardContent className="p-6">
              <h2 className="text-2xl font-semibold">{sword.name}</h2>
              <p className="text-gray-400">Value: {sword.value}</p>
              <p className="text-gray-400">Rarity: {sword.rarity}</p>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="mt-8 text-center">
        <Button variant="primary" className="flex items-center gap-3 bg-yellow-500 hover:bg-yellow-600 text-black font-bold py-3 px-6 rounded-lg transition-transform duration-300 hover:scale-110">
          <DollarSign className="w-6 h-6" /> Donate to Support
        </Button>
      </div>
    </div>
  );
}
