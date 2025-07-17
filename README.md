// SmartZone Trader - React Frontend with TailwindCSS

import React, { useState, useEffect } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Input } from "@/components/ui/input"; import { LineChart, Line, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";

const mockData = [ { time: "09:00", price: 100 }, { time: "10:00", price: 105 }, { time: "11:00", price: 98 }, { time: "12:00", price: 110 }, { time: "13:00", price: 102 }, { time: "14:00", price: 108 }, ];

export default function Home() { const [support, setSupport] = useState(98); const [resistance, setResistance] = useState(110); const [price, setPrice] = useState(105);

useEffect(() => { // Normally you'd fetch real-time price data here }, []);

const getSignal = () => { if (price <= support + 1) return "📉 Buy Zone (Support Reached)"; if (price >= resistance - 1) return "📈 Sell Zone (Resistance Hit)"; return "⚠️ Neutral Zone - Wait"; };

return ( <div className="min-h-screen bg-gray-100 p-4"> <h1 className="text-3xl font-bold text-center mb-6">SmartZone Trader</h1>

<div className="grid grid-cols-1 md:grid-cols-2 gap-6">
    <Card>
      <CardContent>
        <h2 className="text-xl font-semibold mb-4">Live Price Chart</h2>
        <ResponsiveContainer width="100%" height={250}>
          <LineChart data={mockData}>
            <XAxis dataKey="time" />
            <YAxis />
            <Tooltip />
            <Line type="monotone" dataKey="price" stroke="#3b82f6" strokeWidth={2} />
          </LineChart>
        </ResponsiveContainer>
      </CardContent>
    </Card>

    <Card>
      <CardContent>
        <h2 className="text-xl font-semibold mb-4">Support & Resistance</h2>
        <div className="space-y-3">
          <Input
            type="number"
            placeholder="Support Level"
            value={support}
            onChange={(e) => setSupport(Number(e.target.value))}
          />
          <Input
            type="number"
            placeholder="Resistance Level"
            value={resistance}
            onChange={(e) => setResistance(Number(e.target.value))}
          />
          <Input
            type="number"
            placeholder="Current Price"
            value={price}
            onChange={(e) => setPrice(Number(e.target.value))}
          />
          <p className="text-lg font-medium">Signal: <span className="font-bold">{getSignal()}</span></p>
        </div>
      </CardContent>
    </Card>
  </div>
</div>

); }
