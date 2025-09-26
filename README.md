# Assignment Submission – Laravel + Selenium + HTML Integration

## 📌 Overview
This assignment consists of **3 tasks**:
1. Set up the Laravel project and database, verify the login page.
2. Automate the login page with Python Selenium.
3. Integrate an external HTML template page (`app-calendar.html`) into Laravel as a route `/html-page`.

---

##  Task 1: Laravel Project Setup & Login Page
- Downloaded and extracted the given Laravel project.
- Imported `db.sql` into MySQL database.
- Configured `.env` to connect with database.
- Served project locally at:  
  - `http://127.0.0.1:8000/login`

📷 **Screenshot**:  

<img width="1919" height="1024" alt="Screenshot 2025-09-25 231707" src="https://github.com/user-attachments/assets/ed1c02a7-40d7-4961-8a29-6c78baa5b20f" />

---

##  Task 2: Python Selenium Script
- Created automation script `login_automation.py`.
- Script opens Laravel login page, fills **random email & password**, and exits.

### Script (`login_automation.py`):
```python
from selenium import webdriver
from selenium.webdriver.common.by import By
import random, string, time


driver = webdriver.Chrome()
driver.get("http://127.0.0.1:8000/login")
print("Opening http://127.0.0.1:8000/login")


email = f"auto_{''.join(random.choices(string.ascii_lowercase + string.digits, k=8))}@example.com"
password = ''.join(random.choices(string.ascii_lowercase + string.digits, k=10))


driver.find_element(By.NAME, "email_address").send_keys(email)
print(f"Filling email: {email}")
driver.find_element(By.NAME, "password").send_keys(password)
print(f"Filling password: {password}")

time.sleep(2)
driver.quit()
print("Done — closing browser.")
```
 **Screenshot**:
<img width="1076" height="397" alt="Screenshot 2025-09-26 022424" src="https://github.com/user-attachments/assets/c562a2a1-ba17-4646-ad14-635184bad1ad" />

##  Task 3: HTML Calendar Integration

### Steps Completed
1. Downloaded and extracted the provided HTML template.  
2. Copied file:  
   `html/vertical-menu-template/app-calendar.html` →  
   `resources/views/html/app-calendar.blade.php`  
3. Registered a new Laravel route in `routes/web.php`:
   ```php
   Route::get('/html-page', function () {
       return view('html.app-calendar');
   });
```
📷 **Screenshot**:
<img width="1917" height="1034" alt="Screenshot 2025-09-26 114707" src="https://github.com/user-attachments/assets/51613344-59b4-4816-a08e-6d7fbdbccaba" />

<img width="1919" height="1031" alt="Screenshot 2025-09-26 145129" src="https://github.com/user-attachments/assets/23d80411-764b-4b4c-9a58-97d8511d8857" />


##  How to Run
1. Import Database
```
mysql -u root -p laravel_db < db.sql
```
2. Configure .env

Update database credentials inside .env file.

3. Run Laravel Server
```
php artisan serve
```
4. Access Pages
```
Login page → http://127.0.0.1:8000/login

Calendar page → http://127.0.0.1:8000/html-page
```
5. Run Selenium Test
```
python login_automation.py
```

