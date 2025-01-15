import mysql.connector as sqltor


def connect():
  while True:
    un = input('User name: ')
    pswd=input('Password: ')
    try:
        conn=sqltor.connect(host='localhost',user=un ,passwd=pswd )
        print('Connected succefully')
        return conn
    except sqltor.Error as err:  # Learn this. More specific exception handling
            print(f"Error connecting to MySQL: {err}")
      
def checkDB(dbname,cursor,conn):
    cursor.execute("SHOW DATABASES LIKE '{}';".format(dbname)) 
    result=cursor.fetchone()
    if not result:
        createDB(cursor,conn)
    return

def createDB(cursor,conn):
    try:
        cursor.execute("CREATE DATABASE Contact_Manager;")
        conn.commit()
        cursor.execute("USE Contact_Manager;")
        cursor.execute("""
            CREATE TABLE CONTACTS (
                NAME VARCHAR(20) NOT NULL,
                MOBILE_NO VARCHAR(12) NOT NULL PRIMARY KEY,
                EMAIL VARCHAR(40)
            ); """)
        conn.commit()
    except sqltor.Error as err:
        print(f"Error creating database or table: {err}")
    
def addContact(cursor,conn):
    try:
        name=input('Enter name: ')
        mob=input('Enter mobile no.: ')
        email=input('Enter email address: ')
        cursor.execute("INSERT INTO CONTACTS VALUES('{}','{}','{}');".format(name,mob,email))
        conn.commit()
    except sqltor.Error as err:
        print(f"Error creating database or table: {err}")

def viewContacts(cursor):
    cursor.execute("SELECT * FROM CONTACTS;")
    result=cursor.fetchall()
    for i in result:
        print(i)

def searchContact(cursor):
    print('1: SEARCH BY NAME')
    print('2: SEARCH BY MOBILE NUMBER')
    n=int(input("Enter option number: "))
    if n==1:
        name=input("Enter name:")
        cursor.execute("SELECT * FROM CONTACTS WHERE name LIKE %s", ("%" + name + "%",))
        result=cursor.fetchall()
        print(result)
    elif n==2:
        mob=input("Enter mobile number: ")
        cursor.execute("SELECT * FROM CONTACTS WHERE mobile_no ='{}';".format(mob))
        result=cursor.fetchall()
        print(result)
    else:
        print("Invalid choice.")


conn = connect()
cursor = conn.cursor()
dbname = 'Contact_Manager'
checkDB(dbname, cursor,conn)
cursor.execute(f"USE {dbname};")


while True:
    print('-'*50,'\n')
    print("1.Add contact")
    print("2.View contacts")
    print("3.Search conatact")
    print("4.Exit")

    ch=int(input("Enter option number: "))
    if ch==1:
        addContact(cursor, conn)
    elif ch==2:
        viewContacts(cursor)
    elif ch==3:
        searchContact(cursor)
    elif ch==4:
        print("Program terminates...")
        break
    else:
        print("Invalid choice")
conn.close()
