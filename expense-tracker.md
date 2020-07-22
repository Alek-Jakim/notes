```javascript
    const account = {
    name: 'Alek Jakimovski',
    expenses: [],
    income: [],
    addExpense(desc, amount) {
        let expense = {
            service: desc,
            amount: amount
        }
        this.expenses.push(expense);
    }, getAccountSummary() {
        let totalExpenses = 0;
        let totalIncome = 0;

        this.expenses.forEach((expense) => {
            totalExpenses += expense.amount;
        });

        this.income.forEach((inc) => {
            totalIncome += inc.amount;
        })

        const accountBalance = totalIncome - totalExpenses;

        return `${this.name} has $${totalIncome} of income and $${totalExpenses} in expenses. Current balance: $${accountBalance}`
    },
    addIncome(desc, amount) {
        let income = {
            service: desc,
            amount: amount
        }
        this.income.push(income);
    }
}



//Expense -> desc, amount
//Add Expense -> desc, amount
//getAccountSummary -> total up all account expenses || ex: user has $$ in expenses



//Income
// account.addIncome('BIBO', 325);
// account.addIncome('UpWork', 120);
// account.addIncome('Janitor Services', 20);

// console.log(account.income); //all income

//Expenses
// account.addExpense('Coffee', 2.5);
// account.addExpense('Electricity bills', 120.5);
// account.addExpense('Udemy courses', 32.5);
// account.addExpense('Peanut Buter', 8.5);

// console.log(account.expeses); //all expenses

console.log(account.getAccountSummary())


```