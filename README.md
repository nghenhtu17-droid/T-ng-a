import React, { useMemo, useState } from 'react';

export default function App() {
  const [user, setUser] = useState('Dao Huu');
  const [realm, setRealm] = useState('Luyen Khi');
  const [stones, setStones] = useState(500);
  const [gold, setGold] = useState(100);

  const [items, setItems] = useState([
    { name: 'Kiem Thanh Quang', value: 300 },
    { name: 'Dan Duoc', value: 120 }
  ]);

  const total = useMemo(
    () =>
      Number(stones) +
      Number(gold) +
      items.reduce((a, b) => a + Number(b.value || 0), 0),
    [stones, gold, items]
  );

  const addItem = () =>
    setItems([...items, { name: 'Phap Bao Moi', value: 0 }]);

  const updateItem = (i, key, val) =>
    setItems(
      items.map((it, idx) =>
        idx === i ? { ...it, [key]: val } : it
      )
    );

  const removeItem = (i) =>
    setItems(items.filter((_, idx) => idx !== i));

  return (
    <div className="min-h-screen bg-slate-950 text-white p-6">
      <div className="max-w-4xl mx-auto space-y-6">

        <h1 className="text-3xl font-bold">
          Táng Địa - Quản Lý Tài Sản
        </h1>

        <div className="grid md:grid-cols-2 gap-4">

          <div className="bg-slate-900 rounded-2xl p-4">
            <h2 className="font-semibold mb-3">Hồ Sơ</h2>

            <input
              className="w-full mb-2 p-2 rounded bg-slate-800"
              value={user}
              onChange={(e) => setUser(e.target.value)}
            />

            <input
              className="w-full p-2 rounded bg-slate-800"
              value={realm}
              onChange={(e) => setRealm(e.target.value)}
            />
          </div>

          <div className="bg-slate-900 rounded-2xl p-4">
            <h2 className="font-semibold mb-3">Tài Sản</h2>

            <input
              type="number"
              className="w-full mb-2 p-2 rounded bg-slate-800"
              value={stones}
              onChange={(e) => setStones(e.target.value)}
              placeholder="Linh Thạch"
            />

            <input
              type="number"
              className="w-full p-2 rounded bg-slate-800"
              value={gold}
              onChange={(e) => setGold(e.target.value)}
              placeholder="Vàng"
            />
          </div>

        </div>

        <div className="bg-slate-900 rounded-2xl p-4">
          <div className="flex justify-between items-center mb-3">
            <h2 className="font-semibold">Pháp Bảo</h2>

            <button
              onClick={addItem}
              className="px-3 py-1 bg-indigo-600 rounded"
            >
              Thêm
            </button>
          </div>

          <div className="space-y-2">
            {items.map((it, i) => (
              <div key={i} className="grid grid-cols-12 gap-2">

                <input
                  className="col-span-7 p-2 rounded bg-slate-800"
                  value={it.name}
                  onChange={(e) =>
                    updateItem(i, 'name', e.target.value)
                  }
                />

                <input
                  type="number"
                  className="col-span-3 p-2 rounded bg-slate-800"
                  value={it.value}
                  onChange={(e) =>
                    updateItem(i, 'value', e.target.value)
                  }
                />

                <button
                  onClick={() => removeItem(i)}
                  className="col-span-2 bg-red-600 rounded"
                >
                  Xóa
                </button>

              </div>
            ))}
          </div>
        </div>

        <div className="bg-amber-500 text-black rounded-2xl p-6">
          <p className="text-xl font-bold">{user}</p>
          <p>{realm}</p>

          <p className="text-2xl font-bold mt-2">
            Tổng Tài Sản: {total}
          </p>
        </div>

      </div>
    </div>
  );
}
