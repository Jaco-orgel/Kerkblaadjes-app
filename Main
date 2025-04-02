import { useState } from "react";
import { Button } from "@/components/ui/button";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { CheckCircle, Trash2, Pencil, PlusCircle } from "lucide-react";

export default function KrantenwijkApp() {
  const [neighborhoods, setNeighborhoods] = useState({});
  const [newNeighborhood, setNewNeighborhood] = useState("");
  const [selectedNeighborhood, setSelectedNeighborhood] = useState(null);
  const [newAddress, setNewAddress] = useState("");
  const [checked, setChecked] = useState({});
  const [editingIndex, setEditingIndex] = useState(null);
  const [editValue, setEditValue] = useState("");
  const [insertIndex, setInsertIndex] = useState(null);
  const [insertValue, setInsertValue] = useState("");

  const addNeighborhood = () => {
    if (newNeighborhood.trim() !== "" && !neighborhoods[newNeighborhood]) {
      setNeighborhoods({ ...neighborhoods, [newNeighborhood]: [] });
      setNewNeighborhood("");
    }
  };

  const addAddress = (index = null) => {
    if (selectedNeighborhood && newAddress.trim() !== "") {
      const updatedAddresses = [...neighborhoods[selectedNeighborhood]];
      if (index !== null) {
        updatedAddresses.splice(index, 0, newAddress);
      } else {
        updatedAddresses.push(newAddress);
      }
      setNeighborhoods({ ...neighborhoods, [selectedNeighborhood]: updatedAddresses });
      setNewAddress("");
    }
  };

  const removeAddress = (index) => {
    if (selectedNeighborhood) {
      setNeighborhoods({
        ...neighborhoods,
        [selectedNeighborhood]: neighborhoods[selectedNeighborhood].filter((_, i) => i !== index),
      });
    }
  };

  const toggleCheck = (index) => {
    setChecked({ ...checked, [index]: !checked[index] });
  };

  const startEditing = (index, address) => {
    setEditingIndex(index);
    setEditValue(address);
  };

  const saveEdit = (index) => {
    if (selectedNeighborhood && editValue.trim() !== "") {
      const updatedAddresses = [...neighborhoods[selectedNeighborhood]];
      updatedAddresses[index] = editValue;
      setNeighborhoods({ ...neighborhoods, [selectedNeighborhood]: updatedAddresses });
      setEditingIndex(null);
      setEditValue("");
    }
  };

  return (
    <div className="p-6 max-w-lg mx-auto">
      <h1 className="text-xl font-bold mb-4">Krantenwijk App</h1>
      
      <div className="flex gap-2 mb-4">
        <Input
          value={newNeighborhood}
          onChange={(e) => setNewNeighborhood(e.target.value)}
          placeholder="Nieuwe wijk toevoegen"
        />
        <Button onClick={addNeighborhood}>Toevoegen</Button>
      </div>
      
      <div className="mb-4">
        <h2 className="font-bold">Selecteer wijk:</h2>
        <select onChange={(e) => setSelectedNeighborhood(e.target.value)} className="border p-2 rounded w-full">
          <option value="">-- Kies een wijk --</option>
          {Object.keys(neighborhoods).map((neighborhood) => (
            <option key={neighborhood} value={neighborhood}>{neighborhood}</option>
          ))}
        </select>
      </div>

      {selectedNeighborhood && (
        <>
          <div className="flex gap-2 mb-4">
            <Input
              value={newAddress}
              onChange={(e) => setNewAddress(e.target.value)}
              placeholder="Adres toevoegen"
            />
            <Button onClick={() => addAddress()}>Toevoegen</Button>
          </div>
          <ul>
            {neighborhoods[selectedNeighborhood].map((address, index) => (
              <li key={index} className="flex justify-between items-center p-2 border rounded-lg mb-2">
                {editingIndex === index ? (
                  <>
                    <Input value={editValue} onChange={(e) => setEditValue(e.target.value)} className="mr-2" />
                    <Button size="icon" variant="ghost" onClick={() => saveEdit(index)}>
                      ✅
                    </Button>
                  </>
                ) : (
                  <>
                    <span className={checked[index] ? "line-through" : ""}>{address}</span>
                    <div className="flex gap-2">
                      <Button size="icon" variant="ghost" onClick={() => toggleCheck(index)}>
                        <CheckCircle className={checked[index] ? "text-green-500" : "text-gray-500"} />
                      </Button>
                      <Button size="icon" variant="ghost" onClick={() => startEditing(index, address)}>
                        <Pencil className="text-blue-500" />
                      </Button>
                      <Button size="icon" variant="ghost" onClick={() => removeAddress(index)}>
                        <Trash2 className="text-red-500" />
                      </Button>
                      <Button size="icon" variant="ghost" onClick={() => setInsertIndex(index)}>
                        <PlusCircle className="text-green-500" />
                      </Button>
                    </div>
                  </>
                )}
                {insertIndex === index && (
                  <div className="flex gap-2 mt-2">
                    <Input value={insertValue} onChange={(e) => setInsertValue(e.target.value)} placeholder="Nieuw adres invoegen" />
                    <Button onClick={() => { addAddress(index); setInsertIndex(null); setInsertValue(""); }}>Invoegen</Button>
                  </div>
                )}
              </li>
            ))}
          </ul>
        </>
      )}
    </div>
  );
}
