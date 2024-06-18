
# Payroll Management System

## Overview

This Payroll Management System is a Python-based GUI application designed to help manage employee payroll calculations. Users can enter employee details, calculate weekly wages, taxes, and overtime, and generate a payslip. The system ensures accuracy and efficiency in payroll management.

## Features

- **Employee Information Entry**: Input fields for employee name, address, employer, NI number, hours worked, and hourly wage.
- **Wage Calculation**: Automatically calculates weekly wages based on hours worked and hourly rate.
- **Tax Calculation**: Computes the tax amount to be deducted from the gross pay.
- **Overtime Calculation**: Calculates overtime pay for hours worked beyond the standard 40-hour workweek.
- **Payslip Generation**: Generates a detailed payslip with all relevant information and calculations.
- **User-Friendly Interface**: Simple and intuitive interface for easy navigation and use.

## Project Structure

```sh
PayrollManagementSystem/
│
├── main.py                # Main Python script containing the application code
├── README.md              # Project description and instructions

## Setup Instructions

1. **Clone the repository**:
   ```sh
   git clone https://github.com/yourusername/PayrollManagementSystem.git
   cd PayrollManagementSystem
   ```

2. **Install dependencies**:
   Ensure you have Python installed. If not, download and install it from [Python's official website](https://www.python.org/downloads/).

3. **Run the application**:
   ```sh
   python main.py
   ```

## Usage

1. **Enter Employee Details**:
   - Fill in the fields for Name, Address, Employer, NI Number, Hours Worked, and Hourly Rate.

2. **Calculate Wages**:
   - Click on the "Weekly Salary" button to calculate the weekly wages, taxes, and overtime.

3. **View Payslip**:
   - Click on the "View Payslip" button to generate and display the payslip in the text area.

4. **Reset Form**:
   - Click on the "Reset" button to clear all input fields and reset the form.

5. **Exit Application**:
   - Click on the "Exit System" button to close the application.

## Code Explanation

### Functions

#### `enterinfo()`
This function deletes the existing content in the payslip text area and inserts the employee details along with the calculated pay information into the payslip.

```python
def enterinfo():
    txtpayslip.delete("1.0", END)
    txtpayslip.insert(END, "\t\tPay Slip\n\n")
    txtpayslip.insert(END, "Name:\t\t" + Name.get() + "\n\n")
    txtpayslip.insert(END, "Address:\t\t" + Address.get() + "\n\n")
    txtpayslip.insert(END, "Employer:\t\t" + Employer.get() + "\n\n")
    txtpayslip.insert(END, "NI Number:\t\t" + NINumber.get() + "\n\n")
    txtpayslip.insert(END, "Hours Worked:\t\t" + HoursWorked.get() + "\n\n")
    txtpayslip.insert(END, "Net Payable:\t\t" + NetPayable.get() + "\n\n")
    txtpayslip.insert(END, "Wages per hour:\t\t" + wageshour.get() + "\n\n")
    txtpayslip.insert(END, "Tax Paid:\t\t" + Taxable.get() + "\n\n")
    txtpayslip.insert(END, "Payable:\t\t" + Payable.get() + "\n\n")
```

#### `weeklywages()`
This function calculates the weekly wages, tax, net pay, and overtime pay based on the hours worked and hourly rate.

```python
def weeklywages():
    txtpayslip.delete("1.0", END)
    hoursworkedperweek = float(HoursWorked.get())
    wagesperhours = float(wageshour.get())
    paydue = wagesperhours * hoursworkedperweek
    paymentdue = "INR " + str('%.2f' % paydue)
    Payable.set(paymentdue)

    tax = paydue * 0.2
    taxable = "INR " + str('%.2f' % tax)
    Taxable.set(taxable)

    netpay = paydue - tax
    netpays = "INR " + str('%.2f' % netpay)
    NetPayable.set(netpays)

    if hoursworkedperweek > 40:
        overtimehours = (hoursworkedperweek - 40) * wagesperhours * 1.5
        overtime = "INR " + str('%.2f' % overtimehours)
        OverTimeBonus.set(overtime)
    else:
        overtimepay = 0
        overtimehrs = "INR " + str('%.2f' % overtimepay)
        OverTimeBonus.set(overtimehrs)
    return
```

### Variables

The following StringVar() variables are used to store input data and calculated results.

```python
Name = StringVar()
Address = StringVar()
HoursWorked = StringVar()
wageshour = StringVar()
Payable = StringVar()
Taxable = StringVar()
NetPayable = StringVar()
GrossPayable = StringVar()
OverTimeBonus = StringVar()
Employer = StringVar()
NINumber = StringVar()
TimeOfOrder = StringVar()
DateOfOrder = StringVar()
DateOfOrder.set(time.strftime("%d/%m/%Y"))
```

### Widgets

#### Labels

Various labels are used to indicate the different fields in the form.

```python
lblName = Label(fla, text="Name", font=('arial', 16, 'bold'), bd=20, fg="#303030", bg="#88EEDS").grid(row=0, column=0)
lblAddress = Label(fla, text="Address", font=("arial", 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EBBEDS").grid(row=0, column=2)
lblEmployer = Label(fla, text="Employer", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEED5").grid(row=1, column=0)
lblNINumber = Label(fla, text="NI Number", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEEDS").grid(row=1, column=2)
lblHoursWorked = Label(fla, text="Hours Worked", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEEDS").grid(row=2, column=0)
lblHourlyRate = Label(fla, text="Hourly Rate", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEEDS").grid(row=2, column=2)
lblTax = Label(fla, text="Tax", font=('arial', 16, 'bold'), bd=20, anchor='w', fg="#3D3D3D", bg="#EEEED5").grid(row=3, column=0)
lbloverTime = Label(fla, text="OverTime", font=('arial', 16, 'bold'), bd=20, fg="#303030", bg="#EEEED5").grid(row=3, column=2)
lblGrossPay = Label(fla, text="GrossPay", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEEDS").grid(row=4, column=0)
lblNetPay = Label(fla, text="Net Pay", font=('arial', 16, 'bold'), bd=20, fg="#3D3D3D", bg="#EEEED5").grid(row=4, column=2)
```

#### Entry Fields

Entry fields are provided for user input.

```python
etxname = Entry(fla, textvariable=Name, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxname.grid(row=0, column=1)
etxaddress = Entry(fla, textvariable=Address, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxaddress.grid(row=0, column=3)
etxemployer = Entry(fla, textvariable=Employer, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxemployer.grid(row=1, column=1)
etxhoursworked = Entry(fla, textvariable=HoursWorked, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxhoursworked.grid(row=2, column=1)
etxwagesperhours = Entry(fla, textvariable=wageshour, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxwagesperhours.grid(row=2, column=3)
etxnin = Entry(fla, textvariable=NINumber, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxnin.grid(row=1, column=3)
etxgrosspay = Entry(fla, textvariable=Payable, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxgrosspay.grid(row=4, column=1)
etxnetpay = Entry(fla, textvariable=NetPayable, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxnetpay.grid(row=4, column=3)
etxtax = Entry(fla, textvariable=Taxable, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxtax.grid(row=3, column=1)
etxovertime = Entry(fla, textvariable=OverTimeBonus, font=('arial', 16, 'bold'), bd=16, width=22, justify='left')
etxovertime.grid(row=3, column=3)
```

#### Text Area

A text area is used to display the generated payslip.

```python
payslip = Label(f2, textvariable=DateOfOrder, font=('arial', 21, 'bold'), fg="#3D3D3D", bg="#EEEED5").grid(row=0, column=0)
txtpayslip = Text(f2, height=22, width=34, bd=16, font=('arial', 13, 'bold'), fg="green", bg="#EEEED5")
txtpayslip.grid(row=1, column=0)
```

#### Buttons

Buttons are provided to calculate weekly wages, reset the form, view the payslip, and exit the system.

```python
btnsalary = Button(flb, text="Weekly Salary", padx=16, pady=16, bd=8, font=('arial', 16, 'bold'), width=14, fg="#3D3D3D", bg="#EEEEDS", command=weeklywages).grid(row=0, column=0)
btnreset = Button(flb, text='Reset', padx=16, pady=16, bd=8, font=('arial', 16, 'bold'), width=14, command=reset, fg="#3D3D3D", bg="#EEEED5").grid(row=0, column=1)
btnpayslip = Button(flb, text='View Payslip', padx=16, pady=16, bd=8, font=('arial', 16, 'bold'), width=14, command=enterinfo, fg="#3D3D3D", bg="#EEEED5").grid(row=0, column=2)
btnexit = Button(flb, text='Exit System', padx=16, pady=16, bd=8, font=('arial', 16, 'bold'), width=14, command=exit, fg="#3D3D3D", bg="#EEEED5").grid(row=0, column=3)
```

## Contact

For any questions or issues, please contact mssonasp@gmail.com
