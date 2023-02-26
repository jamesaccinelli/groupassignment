# Group Assignment <br>

Slides + Demo Video: https://youtu.be/vUTRiDOxtic

Controls for Implementations: <br>
Colour Grading -> U for Main Camera, I for Warm, O for Cool, P for Custom Grades <br>
<br>
Explanations: <br>
<br>
Diffuse Lighting <br>
Objects with diffuse lighting become brighter as they get closer to a light source and vice-versa. Uses the standard lighting model with texture and colour properties to achieve this. We input a texture and set our albedo to our texture multiplied by our colour property. <br>
<br>
Normal Map <br>
Normal Maps contain info about the normal at that UV coordinate, normals are then used by the fragment shader. WE use colour, main texture, bump texture and bump slider properties. Uses the lambert lighting model. We input our main texture and normal map texture. Our albedo is equal to our main texture multiplied by our colour property. Normal is unpacked, converting the rgb values of the normal map to xyz coordinates, and is then multiplied by the slider value. <br>
<br>
Rim Lighting <br>
Calculating the dot product of the object’s normals and view direction to put light around the edge of the object. Our properties include the colour of our rim edge and the intensity of our rim, rimpower. Within a pass we enable the zbuffer and ensure colour writes to RGB and A channels. We use the Lambert Alpha:fade lighting model, which enables the alpha value with the lambert lighting. We input our view direction. In our shader function our rim value is equal to the dot product of the normalized view direction and normal, which is then saturated (restricting value between 0 and 1) and is then subtracted from one. Our emission/colour is the rim colour multiplied  by our rim value we just solved for to the power of our rimpower, and then all multiplied by 10. Lastly , our alpha value is our rim value to the power of our rimpower value. <br>
<br>
Colour Grading <br>
Alters and enhances the colour of an image by changing the colour of a pixel to another colour. Done through the use of LUTs/Lookup Tables. Our properties include a main texture, LUT texture and Contribution Range or, the intensity of the grade. We then ensure there is no culling or depth so that we can see the effects taking place, and we create a vertex and fragment shader. In our appdata, we have our position, aswell as uv coordinates. In our v2f function, we have the same; position and uv coordinates. Our vertex shader transforms our object from object space to clip space. In our fragment shader, our colour is saturated (0<value<1), we add precision to our sampling so we cannot go beyond the limits of the LUT and we calculate the offset to map the image to the LUT. <br>
<br>
Shadows with Ambient + Diffuse Lighting
In this shader we create our own shadows with the use of 2 passes. Our properties include a colour and texture. In our first pass, we create a vertex and fragment shader and we tell unity to ignore lightmaps so we can make our own shadows. In our appdata we have Position, Normal, and UV Coordinates. In our v2f, UV Coordinates, Colour, Position, and Shadow Coordinates. In our vertex shader we calculate our shadow by Converting Normal to World Space, then converting it to something fragment shader can use and our diff value calculates the lighting model -> ambient + diffuse. In our fragment shader, our colour equals our texture property times our colour property. Shadow pixels are calculated by multiplying them by lighing model, and finally Colour is multiplied by shadow and lighting. <br>
<br>
 In our 2nd pass, shadowcaster tells unity we are casting shadows, we also create a Vertex and Fragment Shader. The #pragma multi_compile_shadowcaster executes the shadows. Our appdata contains Position, Normal, and UV Coordinates. In our v2f we make our shadowcaster only hold shadows. In our vertex shader we tell unity to fill the details of our shadows. Lastly in our fragment shader, we send our shadows to the screen. <br>

