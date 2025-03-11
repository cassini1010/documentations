# SMTP in Python:

### Securely send mail using `SMTP_SSL`:

Its a best practice to store the password in the environment variables. When you create a new environment variable on Windows, it's important to note that changes to environment variables usually require restarting any applications or shells that were open before the variable was added.

```python
import smtplib, ssl

port = 465  # For SSL
password = <password>

# Create a secure SSL context
context = ssl.create_default_context()

with smtplib.SMTP_SSL("smtp.gmail.com", port, context=context) as server:
    server.login("my@gmail.com", password)
    # TODO: Send email here
```

### Securely send mail using `starttls()`:

```python
with SMTP('smtp.gmail.com', 587) as smtp:
    smtp.starttls()
    smtp.login(email_Address, os.environ.get("GMAIL_APP_PSWD"))
    smtp.sendmail(email_Address, email_Address, message.encode('utf-8'))
```

`smtp.gmail.com` is the smtp server of GMail.

`smtp.office365.com` is the smtp server of Outlook Mail.
