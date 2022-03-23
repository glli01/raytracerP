# raytracer Public Runnable
For security reasons (and Academic Integrity Reasons) I only included the executable.
If you want to see the private code please email me.

The code can easily be run as ./raytracer "input_file_name.test" > output.ppm

And go to a ppm viewer (many can be found on google) and upload the ppm file or convert it to png


Looking at the test files may give you an idea but here is a comprehensive list of the commands that are supported in the test files (C. Ravi Ramamoorthi, CSE 167)

# Commands
\# comments This is a line of comments. Ignore any line starting with a #.
Blank line The input file can have blank lines that should be ignored.
command parameter1 parameter2 ... The first part of the line is always the command. Based on what the command is, it has certain parameters which should be parsed appropriately.

# Output image Parameters
size width height: The size command must be the first command of the file, which controls the image size.
maxdepth depth: The maximum depth (number of bounces) for a ray (default should be 5).
output filename: The output file to which the image should be written. You can either require this to be specified in the input, or you can use a suitable default like stdout or raytrace.png (The final files should be .png, with the specific names the autograder requests).

# Scene/ Camera Parameters
camera lookfromx lookfromy lookfromz lookatx lookaty lookatz upx upy upz fov specifies the camera.
sphere x y z radius Defines a sphere with a given position and radius.
maxverts number Defines a maximum number of vertices for later triangle specifications.
maxvertnorms number Defines a maximum number of vertices with normals for later specifications. It must be set before vertices with normals are defined. (same discussion as above)
vertex x y z Defines a vertex at the given location. The vertex is put into a pile, starting to be numbered at 0.
vertexnormal x y z nx ny nz Similar to the above, but define a surface normal with each vertex. The vertex and vertexnormal set of vertices are completely independent (as are maxverts and maxvertnorms).
tri v1 v2 v3 Create a triangle out of the vertices involved (which have previously been specified with the vertex command). The vertices are assumed to be specified in counter-clockwise order. Your code should internally compute a face normal for this triangle.
trinormal v1 v2 v3 Same as above but for vertices specified with normals. In this case, each vertex has an associated normal, and when doing shading, you should interpolate the normals for intermediate points on the triangle.

# Transforms
translate x y z A translation 3-vector.
rotate x y z angle Rotate by angle (in degrees) about the given axis as in OpenGL.
scale x y z Scale by the corresponding amount in each axis (a non-uniform scaling).
pushTransform Push the current modeling transform on the stack as in OpenGL. You might want to do pushTransform immediately after setting the camera to preserve the identity transformation.
popTransform Pop the current transform from the stack as in OpenGL. The sequence of popTransform and pushTransform can be used if desired before every primitive to reset the transformation (assuming the initial camera transformation is on the stack as discussed above).

# Light commands
directional x y z r g b The direction to the light source, and the color, as in OpenGL.
point x y z r g b The location of a point source and the color, as in OpenGL.
attenuation const linear quadratic Sets the constant, linear and quadratic attenuations (default 1,0,0) as in OpenGL. By default there is no attenuation (the constant term is 1, linear and quadratic are 0; that's what we mean by 1,0,0).
ambient r g b The global ambient color to be added for each object (default is .2,.2,.2).

# Material properties
diffuse r g b specifies the diffuse color of the surface.
specular r g b specifies the specular color of the surface.
shininess s specifies the shininess of the surface.
emission r g b gives the emissive color of the surface.
