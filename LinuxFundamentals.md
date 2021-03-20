# Linux Fundamentals

#### chmod

``chmod <permissions> <file>``

Three digits:

User, Group, Everyone else

3   , 4    , 1 

-wx, r--    , --x

![image](https://user-images.githubusercontent.com/80155116/111866775-be143700-89d4-11eb-9198-5b9ce9f71f41.png)

``chmod 455 file``

4,5,5

r--r-xr-x

1(x) + 4(r) = 5 (rx)

User can read, Group can read and execute, Everyone else can read and execute.

