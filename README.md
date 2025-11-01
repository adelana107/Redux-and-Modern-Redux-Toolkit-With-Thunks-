🏦 React-Redux Bank App

A simple banking application built with React and Redux Toolkit that demonstrates state management, asynchronous actions, and component interaction using Redux and React-Redux hooks.

🚀 Features

Create a new customer profile with full name and national ID

Deposit and withdraw money

Request and repay loans

Display account balance and loan status

Currency conversion when depositing in non-USD currencies

Global state management using Redux Toolkit and React-Redux

🧩 Project Structure
src/
│
├── features/
│   ├── accounts/
│   │   ├── AccountOperations.js
│   │   ├── BalanceDisplay.js
│   │   └── accountSlice.js
│   │
│   └── customers/
│       ├── CreateCustomer.js
│       ├── Customer.js
│       └── customerSlice.js
│
├── store.js
└── App.js

⚙️ Technologies Used

React (Functional Components + Hooks)

Redux Toolkit

React-Redux

Redux Thunk

JavaScript (ES6+)

Vite / Create React App (depending on setup)

📦 Installation

Clone the repository

git clone https://github.com/yourusername/redux-bank.git
cd redux-bank


Install dependencies

npm install


Run the app

npm run dev


Open your browser at http://localhost:5173
 (for Vite) or http://localhost:3000
 (for CRA)

🧠 How It Works

The app starts with an empty customer state.

Once a customer is created, the user gains access to account operations:

Deposit (supports currency conversion via Frankfurter API
)

Withdraw funds

Request and pay off a loan

Redux Toolkit slices (accountSlice and customerSlice) manage actions and reducers.

The store.js combines both slices and provides the global Redux store to the app.

📁 Example Components
App.js
import CreateCustomer from "./features/customers/CreateCustomer";
import Customer from "./features/customers/Customer";
import AccountOperations from "./features/accounts/AccountOperations";
import BalanceDisplay from "./features/accounts/BalanceDisplay";
import { useSelector } from "react-redux";

function App() {
  const fullName = useSelector((state) => state.customer.fullName);

  return (
    <div>
      <h1>🏦 The React-Redux Bank ⚛️</h1>
      {fullName === "" ? (
        <CreateCustomer />
      ) : (
        <>
          <Customer />
          <AccountOperations />
          <BalanceDisplay />
        </>
      )}
    </div>
  );
}

export default App;

🌐 API Reference

The app uses the Frankfurter API for real-time currency conversion:

GET https://api.frankfurter.app/latest?amount={amount}&from={currency}&to=USD

🧩 Example Redux Logic
Deposit Thunk (in accountSlice.js)
export function deposit(amount, currency = "USD") {
  if (currency === "USD") return { type: "account/deposit", payload: amount };

  return async function (dispatch) {
    dispatch({ type: "account/convertingCurrency" });
    const res = await fetch(
      `https://api.frankfurter.app/latest?amount=${amount}&from=${currency}&to=USD`
    );
    const data = await res.json();
    dispatch({ type: "account/deposit", payload: data.rates.USD });
  };
}

🧰 Dev Tools

Redux DevTools (Browser Extension)

React Developer Tools

🧑‍💻 Author

Adelana Oluwafunmibi Cornelius
💼 Frontend Developer | React & Redux Enthusiast