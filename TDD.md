# Test Driven Development
http://www.marinamele.com/taskbuster-django-tutorial/taskbuster-working-environment-and-start-django-project

## Setup Environemnt
```shell
virtualenv vtest                        <-- Create the python virtual environment for vtests.
tve                                     <-- Alias to activate the vtest virtual environment.
pip install django                      <-- Install Django.
pip install --upgrade selenium          <-- Install selenium.
pip freeze > testrequirements.txt       <-- Exports pip packages.
mkdir functional_tests                  <-- Create the 'functional_tests' directory.
cd functional_tests                     <-- Change directory into the functional_tests directory.
vs all_users.py                         <-- Create a new file called 'all_users.py' and open in Visual Studio Code.
```
Download the chome webdriver to work with selenium: https://sites.google.com/a/chromium.org/chromedriver/downloads. Extract the file and place it into the windows root directory (C:\Windows\).

### First TDD Test
In the `all_users.py` file input the following:
```py
# -*- coding: utf-8 -*-                                         # Indicates the coding of the file.
from selenium import webdriver                                  # Imports 'selenium' and 'unittest', a Python library for testing.
import unittest

class NewVisitorTest(unittest.TestCase):                        # Creats a 'TestCase' class, named 'NewVisitorTest'.

    def setUp(self):                                            # A 'setUp' method that initializes the test.
        self.browser = webdriver.Firefox()                      # Opens the browser.
        self.browser.implicitly_wait(3)                         # Waits 3 seconds if needed (if the page is not loaded).

    def tearDown(self):                                         # A 'tearDown' method that runs after each test.
        self.browser.quit()                                     # Closes the browser.

                                                                # The 'setUp' and 'tearDown' methods run at the beginning and at the end of each 'test' method.

    def test_it_worked(self):                                   # A method that starts with 'test'.
        self.browser.get('http://localhost:8000')
        self.assertIn('Welcome to Django', self.browser.title)  # Asserts that the title of the webpage has 'Welcome to Django' in it.

if __name__ == '__main__':                                      # Only if Python runs the file directly (not imported) it will execute the function 'unittest.main()'.  
                                                                # This function launches the 'unittest Test runner', that identifies the different tests defined by looking for methods that start with 'test'.
    unittest.main(warnings='ignore')                            # The 'unittest.main() function is called with the optional parameter "warnings='ignore'" to avoid a ResourceWarning message.
```
