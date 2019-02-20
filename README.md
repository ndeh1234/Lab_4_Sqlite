# Lab_4_Sqlite

import sqlite3


db = sqlite3.connect('Chainsaw_Juggling_Records_Holders') # Creates database file
cur = db.cursor()   # Creates a cursor object


# Creates a table if not exists

cur.execute('create table if not exists Records_Holders ( NAME TEXT, COUNTRY TEXT,NUMBER OF CATCHES INT  )')

# Populating the Records_Holders table

cur.execute('insert into Records_Holders values ("Ian Stewart","Canada", 94)')
cur.execute('insert into Records_Holders values("Aaron Gregg", "Canada", 88)')
cur.execute('insert into Records_Holders values("Chad Taylor", "USA", 78)')


db.commit() # Saves changes

# Ask user for information for a new record holder

name = input('Enter name for record holder: ')
country = input('Enter country for record holder: ')
catches = int(input(' Enter number of catches: '))

# Provide data as a second argument to .execute, as a tuple of values
cur.execute('insert into Records_Holders values (?, ?, ?)', (name, country, catches))

db.commit()


def search_for_record_holder(self, term):
    # Searches the recorder holder table for name.

    try:
        cur = self._db.cursor()
        search = f'%{name.upper()}%'
        cur.execute('SELECT rowid, * FROM Records_Holders WHERE UPPER(name) like ? OR UPPER(country) like ?', (search, search))
        return self._cursor_to_records_holders(cur)
    except sqlite3.Error as e:
        raise NameError(f'Error searching for name with search term {term}') from e


def update_catches(self, catche):
            """ Updates the Records_Holders tables and removes a name. Raises NameError if name not in database. """
            try:
                with self._db as db:
                    cur = db.cursor()
                    cur.execute('DELETE FROM Records_Holders catche rowid = ?', (catche.id,))
                    if not cur.rowcount:
                        raise CatchError('Tried to delete a catch that doesn\'t exist')
            except sqlite3.Error as e:
                raise CatchError('Error deleting name') from e


cur.execute('select * from Records_Holders')
for row in cur:
    print(row)
db.commit() # Saves changes
db.close()








