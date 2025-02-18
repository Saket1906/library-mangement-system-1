import tkinter as tk
from tkinter import ttk
from tkinter import messagebox
from tkcalendar import Calendar  # Ensure you have tkcalendar installed: pip install tkcalendar

def login():
    user_id = entry_user_id.get()
    password = entry_password.get()

    if user_id == "adm" and password == "adm":
        open_admin_homepage()
    elif user_id == "user" and password == "user":
        open_user_homepage()
    else:
        messagebox.showerror("Login Failed", "Invalid User ID or Password")

def open_admin_homepage():
    login_window.withdraw()  # Hide the login window
    admin_homepage = tk.Toplevel()
    admin_homepage.title("Admin Home Page")

    # Create and place the Maintenance button
    button_maintenance = tk.Button(admin_homepage, text="Maintenance", command=open_maintenance)
    button_maintenance.grid(row=0, column=0, padx=10, pady=10)

    # Create and place the Reports button
    button_reports = tk.Button(admin_homepage, text="Reports", command=open_reports)
    button_reports.grid(row=0, column=1, padx=10, pady=10)

    # Create and place the Transactions button
    button_transactions = tk.Button(admin_homepage, text="Transactions", command=lambda: open_transactions("admin"))
    button_transactions.grid(row=1, column=0, padx=10, pady=10)

    # Create and place the Product Details button
    button_product_details = tk.Button(admin_homepage, text="Product Details", command=open_product_details)
    button_product_details.grid(row=1, column=1, padx=10, pady=10)

    # Create and place the Log Out button
    button_logout = tk.Button(admin_homepage, text="Log Out", command=lambda: logout(admin_homepage))
    button_logout.grid(row=2, column=0, columnspan=2, pady=10)

def open_user_homepage():
    login_window.withdraw()  # Hide the login window
    user_homepage = tk.Toplevel()
    user_homepage.title("User Home Page")

    # Create and place the Reports button
    button_reports = tk.Button(user_homepage, text="Reports", command=open_reports)
    button_reports.grid(row=0, column=0, padx=10, pady=10)

    # Create and place the Transactions button
    button_transactions = tk.Button(user_homepage, text="Transactions", command=lambda: open_transactions("user"))
    button_transactions.grid(row=0, column=1, padx=10, pady=10)

    # Create and place the Product Details button
    button_product_details = tk.Button(user_homepage, text="Product Details", command=open_product_details)
    button_product_details.grid(row=1, column=0, padx=10, pady=10)

    # Create and place the Log Out button
    button_logout = tk.Button(user_homepage, text="Log Out", command=lambda: logout(user_homepage))
    button_logout.grid(row=1, column=1, padx=10, pady=10)

def open_maintenance():
    maintenance_window = tk.Toplevel()
    maintenance_window.title("Maintenance")

    # Create and place the "Housekeeping" button
    button_housekeeping = tk.Button(maintenance_window, text="Housekeeping", command=lambda: messagebox.showinfo("Housekeeping", "Housekeeping Section"))
    button_housekeeping.grid(row=0, column=0, padx=10, pady=10)

    # Create and place the "Membership" button
    button_membership = tk.Button(maintenance_window, text="Membership", command=lambda: messagebox.showinfo("Membership", "Membership Section"))
    button_membership.grid(row=1, column=0, padx=10, pady=10)

    # Create and place the "Books/Movies" button
    button_books_movies = tk.Button(maintenance_window, text="Books/Movies", command=lambda: messagebox.showinfo("Books/Movies", "Books/Movies Section"))
    button_books_movies.grid(row=2, column=0, padx=10, pady=10)

    # Create and place the "User Management" button
    button_user_management = tk.Button(maintenance_window, text="User Management", command=lambda: messagebox.showinfo("User Management", "User Management Section"))
    button_user_management.grid(row=3, column=0, padx=10, pady=10)

    # Create and place the "Back" button
    button_back = tk.Button(maintenance_window, text="Back", command=maintenance_window.destroy)
    button_back.grid(row=4, column=0, padx=10, pady=10)

def open_reports():
    reports_window = tk.Toplevel()
    reports_window.title("Available Reports")

    # Create and place the "Master List of Books" button
    button_books = tk.Button(reports_window, text="Master List of Books", command=lambda: generate_report("Master List of Books"))
    button_books.grid(row=0, column=0, padx=10, pady=10)

    # Create and place the "Master List of Movies" button
    button_movies = tk.Button(reports_window, text="Master List of Movies", command=lambda: generate_report("Master List of Movies"))
    button_movies.grid(row=1, column=0, padx=10, pady=10)

    # Create and place the "Master List of Memberships" button
    button_memberships = tk.Button(reports_window, text="Master List of Memberships", command=lambda: generate_report("Master List of Memberships"))
    button_memberships.grid(row=2, column=0, padx=10, pady=10)

    # Create and place the "Active Issues" button
    button_active_issues = tk.Button(reports_window, text="Active Issues", command=lambda: generate_report("Active Issues"))
    button_active_issues.grid(row=3, column=0, padx=10, pady=10)

    # Create and place the "Overdue Returns" button
    button_overdue_returns = tk.Button(reports_window, text="Overdue Returns", command=lambda: generate_report("Overdue Returns"))
    button_overdue_returns.grid(row=4, column=0, padx=10, pady=10)

    # Create and place the "Pending Issue Requests" button
    button_pending_requests = tk.Button(reports_window, text="Pending Issue Requests", command=lambda: generate_report("Pending Issue Requests"))
    button_pending_requests.grid(row=5, column=0, padx=10, pady=10)

    # Create and place the "Cancel" button
    button_cancel = tk.Button(reports_window, text="Cancel", command=reports_window.destroy)
    button_cancel.grid(row=6, column=0, padx=10, pady=10)

def generate_report(report_type):
    if report_type == "Master List of Books":
        open_master_list_of_books()
    elif report_type == "Master List of Movies":
        open_master_list_of_movies()
    elif report_type == "Master List of Memberships":
        open_master_list_of_memberships()
    elif report_type == "Active Issues":
        open_active_issues()
    elif report_type == "Overdue Returns":
        open_overdue_returns()
    elif report_type == "Pending Issue Requests":
        open_pending_issue_requests()
    else:
        messagebox.showinfo("Report Generated", f"{report_type} report has been generated.")

def open_master_list_of_books():
    books_window = tk.Toplevel()
    books_window.title("Master List of Books")

    # Create a treeview widget to display book details
    tree = ttk.Treeview(books_window, columns=("Serial No", "Name of Book", "Author Name", "Category", "Status", "Cost", "Procurement Date"), show="headings")
    tree.heading("Serial No", text="Serial No")
    tree.heading("Name of Book", text="Name of Book")
    tree.heading("Author Name", text="Author Name")
    tree.heading("Category", text="Category")
    tree.heading("Status", text="Status")
    tree.heading("Cost", text="Cost")
    tree.heading("Procurement Date", text="Procurement Date")
    tree.pack(padx=10, pady=10)

    # Insert sample book data
    books = [
        ("12345", "Book A", "Author A", "Fiction", "Available", "$20", "2023-01-15"),
        ("67890", "Book B", "Author B", "Science", "Issued", "$25", "2023-02-20"),
        ("11223", "Book C", "Author C", "Economics", "Available", "$30", "2023-03-25"),
        ("44556", "Book D", "Author D", "Children", "Available", "$15", "2023-04-10")
    ]

    for book in books:
        tree.insert("", "end", values=book)

    # Create and place the "Back" button
    button_back = tk.Button(books_window, text="Back", command=books_window.destroy)
    button_back.pack(pady=10)

def open_master_list_of_movies():
    movies_window = tk.Toplevel()
    movies_window.title("Master List of Movies")

    # Create a treeview widget to display movie details
    tree = ttk.Treeview(movies_window, columns=("Serial No", "Name of Movie", "Author Name", "Category", "Status", "Cost", "Procurement Date"), show="headings")
    tree.heading("Serial No", text="Serial No")
    tree.heading("Name of Movie", text="Name of Movie")
    tree.heading("Author Name", text="Author Name")
    tree.heading("Category", text="Category")
    tree.heading("Status", text="Status")
    tree.heading("Cost", text="Cost")
    tree.heading("Procurement Date", text="Procurement Date")
    tree.pack(padx=10, pady=10)

    # Insert sample movie data
    movies = [
        ("12345", "Movie A", "Director A", "Action", "Available", "$20", "2023-01-15"),
        ("67890", "Movie B", "Director B", "Comedy", "Issued", "$25", "2023-02-20"),
        ("11223", "Movie C", "Director C", "Drama", "Available", "$30", "2023-03-25"),
        ("44556", "Movie D", "Director D", "Horror", "Available", "$15", "2023-04-10")
    ]

    for movie in movies:
        tree.insert("", "end", values=movie)

    # Create and place the "Back" button
    button_back = tk.Button(movies_window, text="Back", command=movies_window.destroy)
    button_back.pack(pady=10)

def open_master_list_of_memberships():
    memberships_window = tk.Toplevel()
    memberships_window.title("Master List of Memberships")

    # Create a treeview widget to display membership details
    tree = ttk.Treeview(memberships_window, columns=("Membership Id", "Name of Member", "Contact Number", "Contact Address", "Author Card No", "Start Date of Membership", "End Date of Membership", "Status", "Amount Pending"), show="headings")
    tree.heading("Membership Id", text="Membership Id")
    tree.heading("Name of Member", text="Name of Member")
    tree.heading("Contact Number", text="Contact Number")
    tree.heading("Contact Address", text="Contact Address")
    tree.heading("Author Card No", text="Author Card No")
    tree.heading("Start Date of Membership", text="Start Date of Membership")
    tree.heading("End Date of Membership", text="End Date of Membership")
    tree.heading("Status", text="Status")
    tree.heading("Amount Pending", text="Amount Pending")
    tree.pack(padx=10, pady=10)

    # Insert sample membership data
    memberships = [
        ("M001", "John Doe", "123-456-7890", "123 Main St", "A12345", "2023-01-01", "2023-12-31", "Active", "$0"),
        ("M002", "Jane Smith", "987-654-3210", "456 Elm St", "B67890", "2023-02-01", "2023-12-31", "Active", "$10"),
        ("M003", "Alice Johnson", "555-555-5555", "789 Oak St", "C11223", "2023-03-01", "2023-12-31", "Inactive", "$0")
    ]

    for membership in memberships:
        tree.insert("", "end", values=membership)

    # Create and place the "Back" button
    button_back = tk.Button(memberships_window, text="Back", command=memberships_window.destroy)
    button_back.pack(pady=10)

def open_active_issues():
    active_issues_window = tk.Toplevel()
    active_issues_window.title("Active Issues")

    # Create a treeview widget to display active issues
    tree = ttk.Treeview(active_issues_window, columns=("Book Name", "Member Name", "Issue Date", "Return Date"), show="headings")
    tree.heading("Book Name", text="Book Name")
    tree.heading("Member Name", text="Member Name")
    tree.heading("Issue Date", text="Issue Date")
    tree.heading("Return Date", text="Return Date")
    tree.pack(padx=10, pady=10)

    # Insert sample active issues data
    active_issues = [
        ("Book A", "John Doe", "2023-10-01", "2023-10-15"),
        ("Book B", "Jane Smith", "2023-10-05", "2023-10-20"),
        ("Book C", "Alice Johnson", "2023-10-10", "2023-10-25")
    ]

    for issue in active_issues:
        tree.insert("", "end", values=issue)

    # Create and place the "Back" button
    button_back = tk.Button(active_issues_window, text="Back", command=active_issues_window.destroy)
    button_back.pack(pady=10)

def open_overdue_returns():
    overdue_returns_window = tk.Toplevel()
    overdue_returns_window.title("Overdue Returns")

    # Create a treeview widget to display overdue returns
    tree = ttk.Treeview(overdue_returns_window, columns=("Book Name", "Member Name", "Issue Date", "Return Date", "Fine"), show="headings")
    tree.heading("Book Name", text="Book Name")
    tree.heading("Member Name", text="Member Name")
    tree.heading("Issue Date", text="Issue Date")
    tree.heading("Return Date", text="Return Date")
    tree.heading("Fine", text="Fine")
    tree.pack(padx=10, pady=10)

    # Insert sample overdue returns data
    overdue_returns = [
        ("Book A", "John Doe", "2023-10-01", "2023-10-15", "$5"),
        ("Book B", "Jane Smith", "2023-10-05", "2023-10-20", "$10"),
        ("Book C", "Alice Johnson", "2023-10-10", "2023-10-25", "$15")
    ]

    for return_entry in overdue_returns:
        tree.insert("", "end", values=return_entry)

    # Create and place the "Back" button
    button_back = tk.Button(overdue_returns_window, text="Back", command=overdue_returns_window.destroy)
    button_back.pack(pady=10)

def open_pending_issue_requests():
    pending_requests_window = tk.Toplevel()
    pending_requests_window.title("Pending Issue Requests")

    # Create a treeview widget to display pending issue requests
    tree = ttk.Treeview(pending_requests_window, columns=("Book/Movie Name", "Member Name", "Request Date", "Status"), show="headings")
    tree.heading("Book/Movie Name", text="Book/Movie Name")
    tree.heading("Member Name", text="Member Name")
    tree.heading("Request Date", text="Request Date")
    tree.heading("Status", text="Status")
    tree.pack(padx=10, pady=10)

    # Insert sample pending issue requests data
    pending_requests = [
        ("Book A", "John Doe", "2023-10-01", "Pending"),
        ("Movie B", "Jane Smith", "2023-10-05", "Pending"),
        ("Book C", "Alice Johnson", "2023-10-10", "Pending")
    ]

    for request in pending_requests:
        tree.insert("", "end", values=request)

    # Create and place the "Back" button
    button_back = tk.Button(pending_requests_window, text="Back", command=pending_requests_window.destroy)
    button_back.pack(pady=10)

def open_transactions(role):
    transactions_window = tk.Toplevel()
    transactions_window.title("Transactions")

    # Create and place the "Is book available?" button
    button_check_availability = tk.Button(transactions_window, text="Is book available?", command=open_book_availability)
    button_check_availability.grid(row=0, column=0, padx=10, pady=10)

    # Create and place the "Issue book?" button
    button_issue_book = tk.Button(transactions_window, text="Issue book?", command=open_issue_book)
    button_issue_book.grid(row=1, column=0, padx=10, pady=10)

    # Create and place the "Return book?" button
    button_return_book = tk.Button(transactions_window, text="Return book?", command=open_return_book)
    button_return_book.grid(row=2, column=0, padx=10, pady=10)

    # Create and place the "Pay Fine?" button
    button_pay_fine = tk.Button(transactions_window, text="Pay Fine?", command=open_pay_fine)
    button_pay_fine.grid(row=3, column=0, padx=10, pady=10)

    # Create and place the "Home" button
    button_home = tk.Button(transactions_window, text="Home", command=lambda: go_home(role, transactions_window))
    button_home.grid(row=4, column=0, padx=10, pady=10)

    # Create and place the "Log Out" button
    button_logout = tk.Button(transactions_window, text="Log Out", command=lambda: logout(transactions_window))
    button_logout.grid(row=5, column=0, padx=10, pady=10)

def open_book_availability():
    availability_window = tk.Toplevel()
    availability_window.title("Book Availability")

    # Create a frame for the search bar
    frame_search = tk.Frame(availability_window)
    frame_search.pack(padx=10, pady=10)

    # Create and place the search entry
    entry_search = tk.Entry(frame_search, width=30)
    entry_search.grid(row=0, column=0, padx=5, pady=5)

    # Create and place the search button
    button_search = tk.Button(frame_search, text="Search", command=lambda: search_books(entry_search.get(), tree))
    button_search.grid(row=0, column=1, padx=5, pady=5)

    # Create and place the cancel button
    button_cancel = tk.Button(frame_search, text="Cancel", command=availability_window.destroy)
    button_cancel.grid(row=0, column=2, padx=5, pady=5)

    # Create a treeview widget to display book details
    tree = ttk.Treeview(availability_window, columns=("Book Name", "Author Name", "Serial Number", "Available"), show="headings")
    tree.heading("Book Name", text="Book Name")
    tree.heading("Author Name", text="Author Name")
    tree.heading("Serial Number", text="Serial Number")
    tree.heading("Available", text="Available")
    tree.pack(padx=10, pady=10)

    # Insert sample book data
    books = [
        ("A", "Author Name", "12345", "Y"),
        ("B", "Author Name", "67890", "N"),
        ("C", "Author Name", "11223", "Y"),
        ("D", "Author Name", "44556", "Y")
    ]

    for book in books:
        tree.insert("", "end", values=book)

def search_books(query, tree):
    # Dummy function to search books
    for item in tree.get_children():
        tree.delete(item)

    # Sample data for demonstration
    books = [
        ("A", "Author Name", "12345", "Y"),
        ("B", "Author Name", "67890", "N"),
        ("C", "Author Name", "11223", "Y"),
        ("D", "Author Name", "44556", "Y")
    ]

    for book in books:
        if query.lower() in book[0].lower():
            tree.insert("", "end", values=book)

def open_issue_book():
    issue_window = tk.Toplevel()
    issue_window.title("Book Issue")

    # Create and place the "Enter Book Name" label and drop-down
    label_book_name = tk.Label(issue_window, text="Enter Book Name:")
    label_book_name.grid(row=0, column=0, padx=10, pady=10)
    book_names = ["A", "B", "C", "D"]  # Sample book names
    combo_book_name = ttk.Combobox(issue_window, values=book_names)
    combo_book_name.grid(row=0, column=1, padx=10, pady=10)

    # Create and place the "Enter Author" label and text box
    label_author = tk.Label(issue_window, text="Enter Author:")
    label_author.grid(row=1, column=0, padx=10, pady=10)
    entry_author = tk.Entry(issue_window)
    entry_author.grid(row=1, column=1, padx=10, pady=10)

    # Create and place the "Issue Date" label and calendar
    label_issue_date = tk.Label(issue_window, text="Issue Date:")
    label_issue_date.grid(row=2, column=0, padx=10, pady=10)
    cal_issue_date = Calendar(issue_window, selectmode="day")
    cal_issue_date.grid(row=2, column=1, padx=10, pady=10)

    # Create and place the "Return Date" label and calendar
    label_return_date = tk.Label(issue_window, text="Return Date:")
    label_return_date.grid(row=3, column=0, padx=10, pady=10)
    cal_return_date = Calendar(issue_window, selectmode="day")
    cal_return_date.grid(row=3, column=1, padx=10, pady=10)

    # Create and place the "Remarks" label and text area
    label_remarks = tk.Label(issue_window, text="Remarks:")
    label_remarks.grid(row=4, column=0, padx=10, pady=10)
    text_remarks = tk.Text(issue_window, height=4, width=30)
    text_remarks.grid(row=4, column=1, padx=10, pady=10)

    # Create and place the "Cancel" button
    button_cancel = tk.Button(issue_window, text="Cancel", command=issue_window.destroy)
    button_cancel.grid(row=5, column=0, padx=10, pady=10)

    # Create and place the "Confirm" button
    button_confirm = tk.Button(issue_window, text="Confirm", command=lambda: confirm_issue(
        combo_book_name.get(), entry_author.get(), cal_issue_date.get_date(), cal_return_date.get_date(), text_remarks.get("1.0", "end-1c")
    ))
    button_confirm.grid(row=5, column=1, padx=10, pady=10)

def open_return_book():
    return_window = tk.Toplevel()
    return_window.title("Return Book")

    # Create and place the "Enter Book Name" label and drop-down
    label_book_name = tk.Label(return_window, text="Enter Book Name:")
    label_book_name.grid(row=0, column=0, padx=10, pady=10)
    book_names = ["A", "B", "C", "D"]  # Sample book names
    combo_book_name = ttk.Combobox(return_window, values=book_names)
    combo_book_name.grid(row=0, column=1, padx=10, pady=10)

    # Create and place the "Enter Author" label and text box
    label_author = tk.Label(return_window, text="Enter Author:")
    label_author.grid(row=1, column=0, padx=10, pady=10)
    entry_author = tk.Entry(return_window)
    entry_author.grid(row=1, column=1, padx=10, pady=10)

    # Create and place the "Serial No" label and drop-down
    label_serial_no = tk.Label(return_window, text="Serial No:")
    label_serial_no.grid(row=2, column=0, padx=10, pady=10)
    serial_numbers = ["12345", "67890", "11223", "44556"]  # Sample serial numbers
    combo_serial_no = ttk.Combobox(return_window, values=serial_numbers)
    combo_serial_no.grid(row=2, column=1, padx=10, pady=10)

    # Create and place the "Issue Date" label and text box
    label_issue_date = tk.Label(return_window, text="Issue Date (YYYY-MM-DD):")
    label_issue_date.grid(row=3, column=0, padx=10, pady=10)
    entry_issue_date = tk.Entry(return_window)
    entry_issue_date.grid(row=3, column=1, padx=10, pady=10)

    # Create and place the "Return Date" label and calendar
    label_return_date = tk.Label(return_window, text="Return Date:")
    label_return_date.grid(row=4, column=0, padx=10, pady=10)
    cal_return_date = Calendar(return_window, selectmode="day")
    cal_return_date.grid(row=4, column=1, padx=10, pady=10)

    # Create and place the "Remarks" label and text area
    label_remarks = tk.Label(return_window, text="Remarks:")
    label_remarks.grid(row=5, column=0, padx=10, pady=10)
    text_remarks = tk.Text(return_window, height=4, width=30)
    text_remarks.grid(row=5, column=1, padx=10, pady=10)

    # Create and place the "Cancel" button
    button_cancel = tk.Button(return_window, text="Cancel", command=return_window.destroy)
    button_cancel.grid(row=6, column=0, padx=10, pady=10)

    # Create and place the "Confirm" button
    button_confirm = tk.Button(return_window, text="Confirm", command=lambda: confirm_return(
        combo_book_name.get(), entry_author.get(), combo_serial_no.get(), entry_issue_date.get(), cal_return_date.get_date(), text_remarks.get("1.0", "end-1c")
    ))
    button_confirm.grid(row=6, column=1, padx=10, pady=10)

def confirm_return(book_name, author, serial_no, issue_date, return_date, remarks):
    # Dummy function to confirm book return
    if book_name and author and serial_no and issue_date and return_date:
        messagebox.showinfo("Book Returned", f"Book '{book_name}' by {author} (Serial No: {serial_no}) returned on {return_date}.\nIssue Date: {issue_date}\nRemarks: {remarks}")
    else:
        messagebox.showwarning("Input Error", "Please fill in all mandatory fields.")

def open_pay_fine():
    pay_fine_window = tk.Toplevel()
    pay_fine_window.title("Pay Fine")

    # Create and place the "Enter Fine Amount" label and text box
    label_fine_amount = tk.Label(pay_fine_window, text="Enter Fine Amount:")
    label_fine_amount.grid(row=0, column=0, padx=10, pady=10)
    entry_fine_amount = tk.Entry(pay_fine_window)
    entry_fine_amount.grid(row=0, column=1, padx=10, pady=10)

    # Create and place the "Enter Remarks" label and text area
    label_remarks = tk.Label(pay_fine_window, text="Remarks:")
    label_remarks.grid(row=1, column=0, padx=10, pady=10)
    text_remarks = tk.Text(pay_fine_window, height=4, width=30)
    text_remarks.grid(row=1, column=1, padx=10, pady=10)

    # Create and place the "Cancel" button
    button_cancel = tk.Button(pay_fine_window, text="Cancel", command=pay_fine_window.destroy)
    button_cancel.grid(row=2, column=0, padx=10, pady=10)

    # Create and place the "Confirm" button
    button_confirm = tk.Button(pay_fine_window, text="Confirm", command=lambda: confirm_pay_fine(entry_fine_amount.get(), text_remarks.get("1.0", "end-1c")))
    button_confirm.grid(row=2, column=1, padx=10, pady=10)

def confirm_pay_fine(fine_amount, remarks):
    # Validate the fine amount
    if fine_amount:
        try:
            fine_amount = float(fine_amount)
            messagebox.showinfo("Fine Paid", f"Fine of {fine_amount} paid successfully.\nRemarks: {remarks}")
        except ValueError:
            messagebox.showwarning("Input Error", "Please enter a valid fine amount.")
    else:
        messagebox.showwarning("Input Error", "Please enter the fine amount.")

def go_home(role, window):
    window.destroy()
    if role == "admin":
        open_admin_homepage()
    elif role == "user":
        open_user_homepage()

def open_product_details():
    product_details_window = tk.Toplevel()
    product_details_window.title("Product Details")

    # Create a treeview widget
    tree = ttk.Treeview(product_details_window, columns=("Code No From", "Code No To", "Category"), show="headings")
    tree.heading("Code No From", text="Code No From")
    tree.heading("Code No To", text="Code No To")
    tree.heading("Category", text="Category")

    # Insert product details
    products = [
        ("SC(B/M)000001", "SC(B/M)000004", "Science"),
        ("EC(B/M)000001", "EC(B/M)000004", "Economics"),
        ("FC(B/M)000001", "FC(B/M)000004", "Fiction"),
        ("CH(B/M)000001", "CH(B/M)000004", "Children"),
        ("PD(B/M)000001", "PD(B/M)000004", "Personal Development")
    ]

    for product in products:
        tree.insert("", "end", values=product)

    tree.pack(padx=10, pady=10)

def logout(window):
    window.destroy()
    login_window.deiconify()  # Show the login window again

# Create the main login window
login_window = tk.Tk()
login_window.title("Library Management System - Login")

# Create and place the User ID label and entry
label_user_id = tk.Label(login_window, text="User ID:")
label_user_id.grid(row=0, column=0, padx=10, pady=10)
entry_user_id = tk.Entry(login_window)
entry_user_id.grid(row=0, column=1, padx=10, pady=10)

# Create and place the Password label and entry
label_password = tk.Label(login_window, text="Password:")
label_password.grid(row=1, column=0, padx=10, pady=10)
entry_password = tk.Entry(login_window, show="*")
entry_password.grid(row=1, column=1, padx=10, pady=10)

# Create and place the Login button
button_login = tk.Button(login_window, text="Login", command=login)
button_login.grid(row=2, column=0, columnspan=2, pady=10)

# Create and place the Cancel button
button_cancel = tk.Button(login_window, text="Cancel", command=login_window.quit)
button_cancel.grid(row=3, column=0, columnspan=2, pady=10)

# Start the main event loop
login_window.mainloop()
