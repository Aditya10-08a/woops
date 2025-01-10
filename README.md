from flask import Flask, render_template, request, redirect, url_for, flash

app = Flask(__name__)
app.secret_key = "college_login_secret"  # Secret key for session management

# Mock user data (username and password for simplicity)
users = {
    "admin": "admin123",
    "student1": "password1",
    "student2": "password2"
}

@app.route('/')
def home():
    return render_template('login.html')

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form['username']
        password = request.form['password']

        if username in users and users[username] == password:
            flash(f"Welcome, {username}!", "success")
            return redirect(url_for('dashboard'))
        else:
            flash("Invalid username or password. Please try again.", "danger")
            return redirect(url_for('login'))
    return render_template('login.html')

@app.route('/dashboard')
def dashboard():
    return "<h1>Welcome to the College Dashboard</h1><p>This is a secure area!</p>"

if __name__ == '__main__':
    app.run(debug=True)

