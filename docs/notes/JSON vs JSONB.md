# JSON vs JSONB

They are 2 data types supported by postgres. They are mostly same. JSONB is stored as binary. 

## Containment operator is available in JSONB
@> operator is only available for JSONB. 

You can convert your column to JSONB or type cast it on the fly. 

choice between these is a matter of performance at scale. 

ref : 

https://www.compose.com/articles/faster-operations-with-the-jsonb-data-type-in-postgresql/#:~:text=The%20data%20types%20json%20and,string%2C%20but%20as%20binary%20code.
