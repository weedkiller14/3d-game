import pyglet
from pyglet.gl import *

# Set up the window
window = pyglet.window.Window()

# Set up the 3D environment
glEnable(GL_DEPTH_TEST)

# Set up the camera
glMatrixMode(GL_PROJECTION)
glLoadIdentity()
gluPerspective(60, window.width / window.height, 0.1, 1000)
glMatrixMode(GL_MODELVIEW)

# Define a simple cube
cube_vertices = [    (-1, -1, -1),    (1, -1, -1),    (1, 1, -1),    (-1, 1, -1),    (-1, -1, 1),    (1, -1, 1),    (1, 1, 1),    (-1, 1, 1)]

cube_edges = [    (0, 1),    (1, 2),    (2, 3),    (3, 0),    (4, 5),    (5, 6),    (6, 7),    (7, 4),    (0, 4),    (1, 5),    (2, 6),    (3, 7)]

# Define the cube's color
cube_color = (1, 1, 1)

# Define the cube's position and rotation
cube_position = (0, 0, -10)
cube_rotation = (0, 0, 0)

# Define the update function
def update(dt):
    global cube_rotation
    cube_rotation = (cube_rotation[0] + dt * 50, cube_rotation[1] + dt * 30, cube_rotation[2] + dt * 10)

# Define the draw function
def draw():
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)
    glLoadIdentity()

    # Move the camera to the correct position and orientation
    glTranslatef(0, 0, -20)
    glRotatef(30, 1, 0, 0)
    glRotatef(45, 0, 1, 0)

    # Draw the cube
    glPushMatrix()
    glTranslatef(*cube_position)
    glRotatef(*cube_rotation)
    glColor3f(*cube_color)
    glBegin(GL_LINES)
    for edge in cube_edges:
        for vertex in edge:
            glVertex3fv(cube_vertices[vertex])
    glEnd()
    glPopMatrix()

# Set up the update and draw functions as the game loop
pyglet.clock.schedule_interval(update, 1/60)
pyglet.app.run()                  


To run this code, you will need Python 3 installed on your computer, as well as the Pyglet library. You can install Pyglet using pip by running the following command in your terminal or command prompt:
(pip install pyglet) Once you have installed Pyglet, you can run the code by saving it to a file with a .py extension, navigating to the directory where the file is saved in your terminal or command prompt, and then running the following command:
(python filename.py)Make sure to replace filename.py with the name of the file you have saved the code to. The Pyglet window should then appear, displaying a rotating cube.

