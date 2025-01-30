# Lumine
Webbshop 
import React, { useState } from "react";
import { Button } from "@/components/ui/button";

const product = {
  name: "Signature Tee",
  price: 199,
  sizes: ["S", "M", "L", "XL"],
  images: [
    "https://files.cdn.printful.com/upload/product-templates/94/940113f2839a9e93768e0a8564ee47a3_l",
    "https://files.cdn.printful.com/upload/product-templates/0d/0d2b327a1fd71d9b96fb68106e98bac8_l",
    "https://files.cdn.printful.com/upload/product-templates/d2/d22d45346340cb393b8d5c9e7de30a8a_l",
    "https://files.cdn.printful.com/upload/product-templates/6f/6f1190d09591670747358828b81a643d_l",
    "https://files.cdn.printful.com/upload/product-templates/eb/eb3ca2d4cae67d4105b417309a419088_l"
  ],
  description: "En elegant och modern t-shirt för den sofistikerade bäraren. Leveranstid: 4-7 arbetsdagar."
};

export default function Home() {
  const [selectedImage, setSelectedImage] = useState(product.images[0]);
  const [selectedSize, setSelectedSize] = useState(product.sizes[0]);
  const [cart, setCart] = useState([]);
  const [showCart, setShowCart] = useState(false);
  const [checkout, setCheckout] = useState(false);

  const addToCart = () => {
    setCart([...cart, { ...product, size: selectedSize }]);
  };

  const subtotal = cart.reduce((sum, item) => sum + item.price, 0);
  const shippingCost = cart.length > 0 ? 49 : 0;
  const totalPrice = subtotal + shippingCost;

  if (checkout) {
    return (
      <div className="min-h-screen flex flex-col items-center justify-center bg-gray-900 text-white px-6">
        <button onClick={() => setCheckout(false)} className="absolute top-4 left-4 text-lg">⬅ Tillbaka</button>
        <h3 className="text-4xl font-serif mb-6">Kassan</h3>
        <div className="p-4 bg-gray-800 shadow-lg rounded-lg w-full max-w-lg">
          {cart.map((item, index) => (
            <div key={index} className="flex items-center space-x-4">
              <img src={item.images[0]} alt={item.name} className="w-16 h-16 rounded-lg" />
              <p className="text-lg">{item.name} ({item.size}) - {item.price} kr</p>
            </div>
          ))}
          <p className="mt-4 font-semibold">Totalt exkl. frakt: {subtotal} kr</p>
          <p className="mt-4 font-semibold">Frakt: {shippingCost} kr (4-7 arbetsdagar)</p>
          <p className="mt-2 text-xl font-bold">Totalt inkl. frakt: {totalPrice} kr</p>
          <h4 className="mt-6 text-lg font-semibold">Fraktadress</h4>
          <input type="text" placeholder="Mejladress" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Förnamn" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Efternamn" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Gatuadress" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Postnummer" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Postort" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <input type="text" placeholder="Mobilnummer" className="w-full p-2 mt-2 bg-gray-700 rounded" />
          <Button className="mt-4 px-6 py-3 bg-gold text-white rounded-lg">Betala</Button>
        </div>
      </div>
    );
  }

  return (
    <div className="min-h-screen bg-gray-900 text-white relative">
      <button onClick={() => setShowCart(!showCart)} className="fixed top-4 right-4 bg-gray-700 p-2 rounded-lg">🛒 ({cart.length})</button>
      {showCart && (
        <div className="fixed top-12 right-4 bg-gray-800 p-4 rounded-lg shadow-lg w-64">
          {cart.length > 0 ? (
            <>
              {cart.map((item, index) => (
                <div key={index} className="flex items-center space-x-2 border-b pb-2 mb-2">
                  <img src={item.images[0]} alt={item.name} className="w-12 h-12 rounded-lg" />
                  <div>
                    <p className="text-sm">{item.name} ({item.size})</p>
                    <p className="text-xs text-gray-400">{item.price} kr</p>
                  </div>
                </div>
              ))}
              <p className="text-lg font-bold">Totalt exkl. frakt: {subtotal} kr</p>
              <Button onClick={() => setCheckout(true)} className="mt-2 w-full bg-gold text-white py-2 rounded-lg">Till kassan</Button>
            </>
          ) : (
            <p className="text-sm text-gray-400">Varukorgen är tom.</p>
          )}
        </div>
      )}
      <section className="h-screen flex flex-col justify-center items-center text-center bg-cover bg-center" style={{ backgroundImage: "url('https://i.postimg.cc/c6qYrB4Z/image-1.png')" }}>
      </section>
      <section id="product-details" className="py-20 px-10 bg-gray-800">
        <div className="max-w-4xl mx-auto text-center">
          <h3 className="text-4xl font-serif text-white">{product.name}</h3>
          <p className="mt-2 text-lg text-gray-300">{product.description}</p>
          <div className="p-4 bg-gray-700 shadow-lg rounded-lg mt-6">
            <img src={selectedImage} alt={product.name} className="w-full rounded-lg" />
            <div className="flex space-x-2 mt-2 justify-center">
              {product.images.map((image, index) => (
                <img key={index} src={image} alt={Product view ${index + 1}} className="w-16 h-16 rounded-lg cursor-pointer border" onClick={() => setSelectedImage(image)} />
              ))}
            </div>
            <p className="text-lg font-semibold mt-2">{product.price} kr</p>
            <div className="mt-2">
              <label className="block text-sm font-medium text-gray-300">Storlek</label>
              <select value={selectedSize} onChange={(e) => setSelectedSize(e.target.value)} className="mt-1 p-2 border rounded-lg w-full bg-gray-700 text-white">
                {product.sizes.map((size) => (
                  <option key={size} value={size}>{size}</option>
                ))}
              </select>
            </div>
            <Button onClick={addToCart} className="mt-4 px-6 py-3 bg-gold text-white rounded-lg">Lägg till i varukorg</Button>
          </div>
        </div>
      </section>
    </div>
  );
}
