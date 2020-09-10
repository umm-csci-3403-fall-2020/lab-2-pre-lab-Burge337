# Leak report

# Initial thoughts/points to investigate:
# we've lost 46 bytes of memory that were allocated by calloc
# this call was made in line 41 of the strip function, line 62 of is_clean, and line 87 of main

#to find: how is this memory being used? In particular, which function would it make sense to free the memory after?

#fixing the memory leak:
#Main calls is_clean, which calls strip(str). This strip function returns allocated memory to is_clean, so we can't 
#remove it there. The function does not send that allocated memory on to main, so we remove it before returning in 
#is_clean. We add free(cleaned) to our is_clean function, while also checking to make sure it isn't getting passed a
#string instead, which occurs when we hit the empty string in our Strings array.
