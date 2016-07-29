# Random Art With Python And SciPy

I always wanted to play around with the idea of creating and generating *random* art. To experiment and see what fun things can come out of it!

Recently, I created a new alias and had profile pictures to pick. And that is my excuse to generate a random piece of art and use it as a profile picture, because.. I'm bored as fuck?

### Tools

You need an imaging library. I chose SciPy because it is convenient.

```sh
$ sudo apt-get install python-scipy
```

To import it's misc module (which is what we need):

```python
>>> import scipy.misc
```

We would also need Pythons *random*, *numpy* and *math* libs.

### Digital Images Theory

And image is a 2D array (grid) of pixels where each pixel represents a color on the screen. Generally, a pixel is represented by a three-tuple - *(*r*, *g*, *b*)*. Each of these is a non-negative number in the range *[0, 255]*. Thus there are a total of 256<sup>3</sup> distinct colors.

The idea behind the random (pseudo?) art generator is that we will have three randomized functions (*f*, *g*, h) with domain and codomain *[-1, 1] x [-1, 1]*.

At each pixel *(x, y)*, we will determine the color by the three-tuple *(f(x, y), g(x, y), h(x, y))*.

Lets use the following functions:
- *f* -> *sin(πx)*
- *g* -> *cos(πxy)*
- *h* -> *sin(πy)*

We use the factor π because otherwise, the oscillation is slow and the generated picture will be boring.

### PRNG Theory

There is no *true* RNG. We can only achieve a high entropy. This is because everything on a computer is *deterministic*. Which means that if someone determines the current state of the computer, the following state will always be the same.

In a PRNG, the "determined situation" is a single number called the *seed*. It initializes the PRNG, and proceeds to compute a sequence of bits some deadly math.

The PRNG would be to create random recursive function that maps from [-1, 1] to [-1, 1].

### My Code

```python
import scipy.misc
import numpy as np
import math, random

# image properties
width = 300
height = 300
channels = 3

# image object definition
img = np.zeros((height, width, channels), dtype=np.uint8)

# xx and yy are 300x300 tables containing x and y coordinates as values
# mgrid is used to create meshes
xx, yy = np.mgrid[:width, :height]
circle_1 = ((xx - 100) ** 2 + (yy - 100) ** 2 ) ** 1 # play around with these
circle_2 = ((xx - 100) ** 3 + (yy - 100) ** 3 ) ** 1 # functions to chnage the
circle_3 = ((xx - 100) ** 2 + (yy - 100) ** 4 ) ** 1 # output image

# of course, if we actually used the random function as intended
# it would generate recursive functions and we wouldn't need to 
# manually play with the functions to get new images

#set RGB values
for y in range(img.shape[0]):
	for x in range(img.shape[1]):
		r, g, b = circle_1[y][x], circle_2[y][x], circle_3[y][x]
		img[y][x][0] = r
		img[y][x][1] = g
		img[y][x][2] = b

scipy.misc.imshow(img)

rn = random.randint(0,1000)
image_name = "whoa" + str(rn) + ".png"
scipy.misc.imsave(image_name, img)
```

### Generated Images

![1] | ![2] | ![3]
![4] | ![5] | ![6]
![7] | ![8] | ![9]

### To Imgur 
You Suck. Kthanx.

### License 
![CC](https://licensebuttons.net/l/by/3.0/88x31.png)

Except where otherwise noted, content on this site is licensed under a [Creative Commons Attribution 4.0](https://creativecommons.org/licenses/by/4.0/) International license.


[1]: <https://s32.postimg.org/5emwzbsh1/whoa119.png>
[2]: <https://s32.postimg.org/4dmoa7bhh/whoa151.png>
[3]: <https://s32.postimg.org/uagcmtf51/whoa231.png>
[4]: <https://s32.postimg.org/fsj5etntx/whoa236.png>
[5]: <https://s32.postimg.org/dchc0z5r9/whoa461.png>
[6]: <https://s32.postimg.org/ktqjg6vad/whoa488.png>
[7]: <https://s32.postimg.org/bn88swq1x/whoa638.png>
[8]: <https://s32.postimg.org/6puo7so2t/whoa807.png>
[9]: <https://s32.postimg.org/wzkc4bzdx/whoa959.png>