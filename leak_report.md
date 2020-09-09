# Leak report

# Initial thoughts/points to investigate:
# we've lost 46 bytes of memory that were allocated by calloc
# this call was made in line 41 of the strip function, line 62 of is_clean, and line 87 of main

#to find: how is this memory being used? In particular, which function would it make sense to free the memory after?
