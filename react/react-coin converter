import styles from "./App.module.css";
import { useState, useEffect } from "react";

function App() {
  const [loading, setLoading] = useState(true);
  const [coins, setCoins] = useState([]);
  const [amount, setAmount] = useState(0);
  const [currency, setCurrency] = useState(0);

  const onChange = (event) => setCurrency(event.target.value);
  const handleInput = (event) => setAmount(event.target.value);

  useEffect(() => {
    fetch("http://api.coinpaprika.com/v1/tickers")
      .then((response) => response.json())
      .then((json) => {
        setCoins(json);
        setLoading(false);
      });
  }, []);

  return (
    <div className={styles.font}>
      <h1>My Coins {loading ? "" : `(${coins.length})`}</h1>
      {loading ? (
        <strong>Loading ...</strong>
      ) : (
        <>
          <h3>Please select coin to convert </h3>
          <div>
            <select onChange={onChange}>
              <option>Please select currency</option>
              {coins.map((coin) => (
                <option key={coin.id} value={coin.quotes.USD.price.toFixed(2)}>
                  {coin.name} ({coin.symbol}) : $
                  {coin.quotes.USD.price.toFixed(2)} USD
                </option>
              ))}
            </select>
          </div>
          <div>
            <h3>Please enter the amount</h3>
            <input
              onChange={handleInput}
              value={amount}
              type="number"
              placeholder="please write amount in USD"
            ></input>
            {amount ? (
              <h2>You can get {(amount / currency).toFixed(4)}</h2>
            ) : null}
          </div>
        </>
      )}
    </div>
  );
}

export default App;
