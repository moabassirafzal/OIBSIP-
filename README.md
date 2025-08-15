# OIBSIP-
Created a atm interface using java programming 

import java.util.*;
import java.time.LocalDateTime;

// ---------- User Class ----------
class User {
    private String userId;
    private String pin;
    private double balance;

    public User(String userId, String pin, double balance) {
        this.userId = userId;
        this.pin = pin;
        this.balance = balance;
    }

    public String getUserId() {
        return userId;
    }

    public String getPin() {
        return pin;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }
}

// ---------- Transaction Class ----------
class Transaction {
    private String type;
    private double amount;
    private LocalDateTime dateTime;

    public Transaction(String type, double amount) {
        this.type = type;
        this.amount = amount;
        this.dateTime = LocalDateTime.now();
    }

    public String toString() {
        return dateTime + " - " + type + ": $" + amount;
    }
}

// ---------- Bank Class ----------
class Bank {
    private User user;
    private List<Transaction> transactions;

    public Bank(User user) {
        this.user = user;
        this.transactions = new ArrayList<>();
    }

    public void deposit(double amount) {
        if (amount > 0) {
            user.setBalance(user.getBalance() + amount);
            transactions.add(new Transaction("Deposit", amount));
            System.out.println("Deposit successful.");
        } else {
            System.out.println("Invalid amount.");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && user.getBalance() >= amount) {
            user.setBalance(user.getBalance() - amount);
            transactions.add(new Transaction("Withdraw", amount));
            System.out.println("Withdrawal successful.");
        } else {
            System.out.println("Insufficient balance or invalid amount.");
        }
    }

    public void transfer(double amount, String recipientId) {
        if (amount > 0 && user.getBalance() >= amount) {
            user.setBalance(user.getBalance() - amount);
            transactions.add(new Transaction("Transfer to " + recipientId, amount));
