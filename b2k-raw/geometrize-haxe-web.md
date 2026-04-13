## How It Works

			

This webpage uses the [Geometrize Haxe](https://github.com/Tw1ddle/geometrize-haxe/) library to transform images into shapes. It's a demo for [Geometrize](https://www.geometrize.co.uk/), my [open source](https://github.com/Tw1ddle/geometrize) desktop app designed for recreating images as geometric primitives.
			

Given an image to recreate, Geometrize generates hundreds of random shapes, and repeatedly mutates these as part of a hillclimbing optimization approach. Internally, this demo uses a web worker so the webpage remains responsive while the geometrization algorithm ranks thousands of these shapes behind the scenes, only picking the best-fitting shapes for use in the final image.
			

The "Run/Pause" button starts or stops the geometrization process, the "Step" button adds one primitive to the image when pressed, the "Open Image" button lets you select your own images, the "Random Image" button picks a random preset image, and the "Reset" button clears all of the current shapes, restarting the geometrization from scratch. The "Save Image" button saves a PNG of the geometrized image, the "Save SVG" button saves an infinitely scalable vector-based image, and the "Save JSON" button saves the shape data to a JSON text file.
			

Additional controls are accessed by clicking on the "Settings" section. The "Shape Opacity" slider controls the how transparent added shapes are. The "Initial Background Opacity" slider lets you make the initial background image more or less opaque - try turning this down and then hitting the "Reset" button if have an image with a transparent background. The "Random Mutations" and "Shapes Per Step" parameters are adjustable for striking a balance between speed and quality. The "Shape Type" checkboxes allow you to select the shape types used in the final image. To leave an image geometrizing in the background, it is often useful to set the "Max Shape Cap" to your desired number of shapes.
			

For more, see the [list of Geometrize resources](https://resources.geometrize.co.uk/). Also try Geometrizer, the [Twitter bot](https://github.com/Tw1ddle/geometrize-twitter-bot) built on top of the [Geometrize](https://www.geometrize.co.uk/) desktop app.
			

If you have suggestions, requests or comments, please [open an issue](https://github.com/Tw1ddle/geometrize-haxe) or [contact Sam](https://twitter.com/Sam_Twidale).