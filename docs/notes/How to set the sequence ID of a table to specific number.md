# How to set the sequence ID of a table to specific number


Sequence ID autopopulates ID field when a new entry is created
![[Pasted image 20201218115233.png]]

When you import data, and add new entries manually, you need to change the seuquence ID to next value (in this example it's 90000):

```SQL
ALTER SEQUENCE access_id_seq RESTART WITH 90000;
```