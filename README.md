# Transaction Management System

A Swift project to manage financial transactions, including adding, filtering, deleting, and calculating totals for transactions.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Tech Stack](#tech-stack)

## Features

- *Add Transactions*: Add new transactions with details like name, category, price, and date.
- *Add Categories*: Add unique categories to the system.
- *Filter Transactions*: Filter transactions by category.
- *Calculate Totals*: Calculate the total amount of transactions for a specific category.
- *Check Balance: Checking Balance for user

## Installation

1. *Clone the repository*
   sh
   git clone https://github.com/irvanwilly13/Assignmet1_MuhammadIrvanWilly.git
   

2. *Open the project*
   Open the cloned repository in Xcode.

## Usage

Here is an example of how to use the Transaction struct and FinanceManajemen class:

```swift
import UIKit

// MARK: ASSIGNMENT 1

enum TypeTransaction: String {
    case income
    case expense
}

// MARK: Struct of Transaction
struct Transaction {
    var nama: String
    var category: TypeTransaction
    var amount: Double
    var date: Date = .now
}

// MARK: Protocol Finance Manajemen
protocol FinanceManajemen {
    var listTransaction: [Transaction] {get set}
    func checkBalance()
    func totalIncome() -> Double
    func totalExpense() -> Double
    func addTransaction(transaction: Transaction)
    func filterTransaction(byCategory: TypeTransaction)
}

class Transaksi: FinanceManajemen {

    var listTransaction: [Transaction] = []
    
    func addTransaction(transaction: Transaction) {
        listTransaction.append(transaction)
    }
    
    func filterTransaction(byCategory: TypeTransaction) {
        let filterData = listTransaction.filter { $0.category == byCategory }
        
        for i in filterData {
            print(i)
        }
    }
    
    
    func totalIncome() -> Double {
        let filterData = listTransaction.filter { $0.category == .income }
        
        let totalIncome = filterData.reduce(0) { $0 + $1.amount }
        
        return totalIncome
    }
    
    func totalExpense() -> Double {
        let filterData = listTransaction.filter { $0.category == .expense }
        
        let totalExpense = filterData.reduce(0) { $0 + $1.amount }
        
        return totalExpense
    }
    
    func checkBalance() {
        print("total balance ")
        
        let totalIncome = self.totalIncome()
        let totalExpense = self.totalExpense()
        
        let balance = totalIncome - totalExpense
        
        print("Total Balance adalah \(balance)")
    }
}


class Pengguna {
    var nama: String
    var transaksi: Transaksi // diambil dari class Transaksi
    
    init(nama: String, transaksi: Transaksi) {
        self.nama = nama
        self.transaksi = transaksi
    }
    
    func tampilkanPengguna() {
        print("Nama Pengguna: \(self.nama)")
        transaksi.checkBalance()
    }
    
    func tambahTransaksi(nama: String, category: TypeTransaction, amount: Double, date: Date = .now) {
        let balance = transaksi.totalIncome() - transaksi.totalExpense()
        
        if category == .expense && balance < amount {
            print("Transaksi tidak bisa dilakukan. Saldo tidak mencukupi.")
        } else {
            let transaction = Transaction(nama: nama, category: category, amount: amount, date: date)
            transaksi.addTransaction(transaction: transaction)
            print("Transaksi sedang di proses")
        }
    }
}

// MARK: Example Usage

let transaksi1 = Transaksi()
let pengguna1 = Pengguna(nama: "Irvan", transaksi: transaksi1)

let transaksi2 = Transaksi()
let pengguna2 = Pengguna(nama: "Farhan", transaksi: transaksi2)

pengguna1.tambahTransaksi(nama: "Pendapatan", category: .income, amount: 120000)
pengguna1.tambahTransaksi(nama: "Tagihan listrik", category: .expense, amount: 23000)
pengguna1.tampilkanPengguna()

pengguna1.tambahTransaksi(nama: "Bonus", category: .income, amount: 40000)
pengguna1.tampilkanPengguna()

pengguna2.tambahTransaksi(nama: "Tabungan", category: .income, amount: 3000)
pengguna2.tambahTransaksi(nama: "sepatu", category: .expense, amount: 5000)
pengguna2.tampilkanPengguna()

```


## Tech Stack

- *Language*: Swift
- *IDE*: Xcode

