# Performance Statement

Most of this program is pretty light. A punch-in or punch-out just finds one record and writes one record, so the database can do it almost instantly. Here are the numbers I would aim for:

- Punch In and Punch Out: the message shows up within 1 second. People are standing there, and at the start of a shift they're in a line.
- Jobs Completed Report: a full year of data shows up within 3 seconds. This is the heaviest thing a worker can ask for, because the program has to read a lot of records, group them by day, and add everything up.
- The 5:30 PM auto punch-out: nobody is waiting on it, so a few minutes is fine.

A few things could slow it down.

The data keeps growing. With around 50 workers doing about 3 work events a day, that's roughly 37,500 records a year. Not a lot, but if the program has to look through every row each time, it gets a bit slower every year. Adding an index on employee number and date fixes that.

There's only one punch-in computer. At 8 AM everyone needs it at the same time, and a faster program won't fix a line. Keeping punch-in to one screen helps, but ABC might need a second computer.

The program also needs the database to be up. If the network or the database goes down, it should show a clear error instead of just freezing.
