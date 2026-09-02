This is all of my knowledge over the past year working on vehicles for this game. There's probably still things left to learn, but since I'm the first only person who's made cars for FOUC that aren't ports from the other FlatOuts, I'm probably the most qualified to make such a guide.

Working on the Honda Civic from NFS ProStreet, exported with NFS-CarToolkit 3.1 using the “Export checked” option under Geometry for both the car model and the plate model, as well as the “Export all” option under Textures

Importing the fbx into Blender, all default settings:

<img width="1081" height="689" alt="civic_1" src="https://github.com/user-attachments/assets/2c59b278-f435-4022-8802-ba4ecdff48ce" />

Due to the quirks of this model (and all ProStreet models, most of this also applying to other NFS games of this era), it has to be set up pre-conversion:
- Delete all objects starting with a _ except for _BRAKE_FRONT_1, _LICENSE_PLATE_REAR_1, _SEAT_LEFT_1 and_SEAT_RIGHT_1

<img width="301" height="517" alt="civic_2" src="https://github.com/user-attachments/assets/7811ddae-a850-4ff4-811b-7506288fe865" />

- Delete all objects with “WINDTUNNEL” in their name, as well as “KIT00_DRIVER_A”
- Select all remaining objects that start with a _, and use Origin to Geometry to be able to use their positions:

<img width="885" height="279" alt="civic_3" src="https://github.com/user-attachments/assets/558434ea-1b0c-4c2a-a0cf-b138b6d509d3" />

- Select _SEAT_LEFT_1, press Shift+S and click Cursor to Selected

<img width="650" height="330" alt="civic_4" src="https://github.com/user-attachments/assets/7f15c0cb-fb31-4060-b669-e39fcf4055b5" />

- Select KIT00_SEAT_LEFT_A, press Shift+S and click Selection to Cursor. This will move the seat into place

<img width="650" height="330" alt="civic_5" src="https://github.com/user-attachments/assets/6c476f64-567a-4cb3-9414-f627764d5f6c" />

- Do the same with _SEAT_RIGHT_1 to KIT00_SEAT_RIGHT_A, _BRAKE_FRONT_1 to KIT00_BRAKE_FRONT_A, KIT00_BRAKE_REAR_A, KIT00_BRAKEROTOR_FRONT_A and KIT00_BRAKEROTOR_REAR_A, then _LICENSE_PLATE_REAR_1 to PLATES_KIT00_LICENSE_PLATE_A, afterwards delete the empty position objects

- Parent the brakes and brake rotors to the wheels, select all wheel-related objects, duplicate all of it with Shift+D then press Escape, afterwards move the wheels into their correct places

<img width="305" height="207" alt="Screenshot_20251030_174718" src="https://github.com/user-attachments/assets/41393fe4-9d04-4cf9-850c-ed62faf188b2" />

- The plate might need rotating, if so then select it, use Numpad 1 or 3 for the side view and select wireframe shading to then use the rotate tool to line it up with the car, afterwards drag with the middle mouse button to reset the view

<img width="1457" height="790" alt="Screenshot_20251030_155746" src="https://github.com/user-attachments/assets/780c004a-e519-4bb0-9699-4e4ea6c90fb2" />

Now the actual porting process may begin, starting with basic material setup.
There are a few basic patterns to follow for choosing each texture's lighting, all of which are based on the material name.

- Add the "_" prefix to use the 'car metal' shader, for a glossy, plasticy, slightly metallic look, with reflectivity based on the texture's alpha channel
- Add the "interior" prefix to use the 'car diffuse' shader, for a matte look
- Add the "tire" prefix to use the 'car tire' shader, mainly relying on the bumpmap for lighting
- Add the "rim" prefix to use the 'car rim' shader, making the material very shiny
- Add the "window" prefix to use the 'car window' shader, with further exact names for breakable windows being "window_front", "window_rear", "window_left" and "window_right". Use a different name with this prefix for an unbreakable window
- Add the "light" prefix to use the 'car lights' shader, which also forces the texture to lights.dds, using such names as "light_brake_l", "light_brake_m", "light_brake_r", "light_reverse_l", "light_reverse_r", "light_front_l", "light_front_r". These are later configured in the car's lights.ini.
- Add "_alpha" to the end of the name to make the texture's alpha channel be used for transparency, such as for badges (not required for the car window and car lights shaders)
- Name the shader "body" to use the car's changeable skin texture

After these steps comes the UV mapping. FOUC only supports a few select textures for menucars, so if your car uses more than 4 miscellaneous textures, you'll need to do this unless you want to remove parts from the menucar.
This step can be skipped for FO2 cars if you have my car limit adjuster.

FOUC only supports these textures for menucars, so create one or more texture atlases for these:
- tire.dds
- rim.dds
- grille.dds
- interior.dds

Neatly sort all of the miscellaneous texture into one larger texture and save it.
Here's the atlas I made for this car, I chose grille.dds:

<img width="715" height="717" alt="Screenshot_20251030_175842" src="https://github.com/user-attachments/assets/77ddd248-4740-40d4-bfb8-ab8bb5ce81a2" />

The model now has to be lined up to work with this atlas. Click on one part of the model, press A, enter the UV Editing tab up top, and on the right side select the Material tab.

<img width="1920" height="1035" alt="Screenshot_20251030_180022" src="https://github.com/user-attachments/assets/cfaf740f-4360-4159-aa88-d7024625bf35" />

Click on the Open Image button in the left side window, select your atlas.

<img width="775" height="281" alt="Screenshot_20251030_180046" src="https://github.com/user-attachments/assets/b619c9ba-fae8-4d78-9175-6f7209d49e9a" />

Now on the right side, one-by-one select each material that should not be part of the atlas, click the Select button to select all faces with that material and press H while the cursor is in the right side viewport window to hide them.

<img width="1803" height="741" alt="Screenshot_20251030_180414" src="https://github.com/user-attachments/assets/b42e3942-eb1d-4c61-a36b-123ea241f2cf" />

After you've made sure the only visible parts of the model are the ones that use textures on the atlas, repeat this process for each such texture:
- Select all polygons with that material using the same method described earlier
- Hover your cursor over to the UV view on the left side, press A to select everything.
- Pop open the small menu on the top right of the UV view, select the View tab, enable Pixel Coordinates (optional but I prefer it this way) and up top change Pivot to 2D Cursor

<img width="465" height="327" alt="Screenshot_20251030_180604" src="https://github.com/user-attachments/assets/0cccecaa-60de-481f-ae95-ce61975ee9b9" />

- Move the polygons in the UV view to match up with the correct position on the atlas using movement binds to make sure they won't end up offset:
- To scale, press S and then type the amount. Since we're working with an atlas here, the scale amount is usually 0.5, 0.25, or 0.125. To scale on only one axis, press X or Y before typing the number in.
- To move, press G, then X or Y and then type the amount (in either pixels if you've selected pixel coordinates, or fractions such as 0.5 or 0.25 if you didn't)
- Once the UV map is in place, press H while hovering over the right side viewport to hide the modified mesh, and continue with another material until all of them have been moved.
After all of the UV maps have been moved, make sure to change all affected materials to use the atlas as their textures.

<img width="839" height="468" alt="Screenshot_20251030_181615" src="https://github.com/user-attachments/assets/e701f0d0-835d-4a17-9958-c4e1c7e595fd" />

Having set up the materials and UVs, it's time to get the model into the game's format.
Switch back to the Layout tab, use File -> Append and select the base .blend file:
https://drive.google.com/file/d/1_r1PuEzW1BB--D77h8UALXCF44t5qQgJ/view?usp=sharing

Create a new dummy using Add -> Empty -> Plain Axes, then set its position and rotation to 0 on all axes if they're not already
Select all of your car's parts and drag them into the newly created empty while holding Shift and Alt (or only Shift if you're using a newer version of Blender as they've recently stupidly changed Alt to mean "hold down to not keep transforms" rather than "hold down to keep transforms", and in this case you want to keep transforms)

<img width="337" height="311" alt="Screenshot_20251030_201241" src="https://github.com/user-attachments/assets/247ffb3b-f447-4421-a75a-70bf54546f37" />

Scale and rotate the empty until the car matches the scale and rotation of the test car you just imported, the scale is usually 0.01 on all axes. You may delete the test car once this is done.
If it's not already the case, move the empty until the bottom of the car's body is roughly at the origin point of the 3D space, shown by the red and green lines.

<img width="900" height="416" alt="Screenshot_20251030_191726" src="https://github.com/user-attachments/assets/09cd201d-b51a-46a0-a234-df96bbf25445" />

Expand the BGMMesh dummy, select "body", hover the cursor over the viewport and press Shift+D to duplicate it as many times as the amount of separate parts your model should have.
Name these empty parts accordingly, specific parts should follow the game's naming conventions:
- The main body should be called "body" (required) This also includes parts such as lights and windows that are part of the body
- For brakes and other parts of the hub, use "wheelhub_fl", "wheelhub_fr", "wheelhub_rl", "wheelhub_rr" for front left, front right, rear left and rear right, respectively.
- For tires, use "tire_fl", "tire_fr", "tire_rl", "tire_rr" for front left, front right, rear left and rear right, respectively.
- For suspension springs, use "shock_fl", "shock_fr", "shock_rl", "shock_rr" for front left, front right, rear left and rear right, respectively.
- Suspensions should either be "susp_front" and "susp_rear" for combined beam axles or "susp_fl", "susp_fr", "susp_rl" and "susp_rr" for independent suspension
- The steering wheel should be called "steering_wheel" or "steering_wheel_lo"
- The hood should be called "hood", the trunk should be called "trunk", front doors should be called "door_l" and "door_r", the exhaust(s) should be called "exhaust_1", "exhaust_2", etc.
Every other named part will be considered a generic detachable panel and will be searched for in panels.ini for deformation and detach properties. The game will throw an error if any such panels don't have a panels.ini entry.
Refer to vanilla cars' panels.ini files for template data. Most of my cars' panels are simply copy pasted from these.

Add each of your car's parts to the newly created dummies by doing the following:
- (wheelhubs, suspension and tires only) Move the empty dummy to the position you would like its rotation pivot to be. For tires and wheelhubs use the Selection to Cursor method from above to match them with the original tire positions, for suspensions use their closest point to the center of the car.
- (steering wheel only) Move the empty dummy to its correct rotation pivot position, and rotate it the right amount for it to match the tilt of the steering wheel model.
- Select your car's desired part in the list on the right side
- Select the destination in the same list while holding Ctrl
- Press Ctrl + J while hovering over the viewport window to attach the part to the empty dummy
- (hood, trunk, doors and panels only) Select the newly attached part, and use Origin to Geometry to set its center of mass correctly

Next, creating the shadow model. In UC this only affects how large the shadow texture is, so we'll be doing a very simple method:
- Select body_shadow, enter Edit Mode on the top right
- Select Add -> Cube
- Press A to select all of the cube
- Scale and move it until it's roughly the size of the car and encompasses it on all axes, (minus the wheels) wireframe mode recommended
- Go back to Object Mode

<img width="1069" height="458" alt="Screenshot_20251030_201523" src="https://github.com/user-attachments/assets/0631c260-dfd8-40e2-86a1-2b024a6de99c" />

Final step of the model's creation, the dummies. Expand the Objects dummy, and first, move all the existing dummies into their correct positions.
- engine_fire_dummy and engine_smoke_dummy should both be roughly around the middle of the engine block
- The light dummies should be where you'd like each light to get damaged from, and where the flare texture will display. Feel free to delete or add dummies of this type according to what light materials you set up prior.
- The placeholder tire dummies must be where each tire is. Use the Selection to Cursor method to make sure they're set to the same exact positions

Final step of the model's creation, the dummies. Expand the Objects dummy, and first, move all the existing dummies into their correct positions.
- engine_fire_dummy and engine_smoke_dummy should both be roughly around the middle of the engine block
- The light dummies should be where you'd like each light to get damaged from, and where the flare texture will display. Feel free to delete or add dummies of this type according to what light materials you set up prior.
- The placeholder tire dummies must be where each tire is. Use the Selection to Cursor method to make sure they're set to the same exact positions

Once these are done, it's time to export the model. There are 3 models to be exported:

First, export the tire model:
- Save a backup file
- Delete everything under Objects, as well as all car parts except tire_fl, tire_fr, tire_rl and tire_rr
- Export to fbx, all default settings

<img width="1685" height="737" alt="Screenshot_20251030_201722" src="https://github.com/user-attachments/assets/63bca92a-1cae-4918-84ea-5119e9ef78ff" />

Afterwards, reload the backup and export the menu model, which is a bit more complicated:
- Delete body_shadow and everything under Objects
- Select body in the right side window
- Press A to select all other objects, press Ctrl + J while hovering over the viewport to join all of them into a single object
- Minimze material count, menucars only support around 16 different materials:
- Make sure that no identical materials exist, such as multiple materials using the same shader and texture. If any do, move them into one clump using the up/down arrows in the material list, and then delete each duplicate until only the topmost one remains. The affected polygons will automatically be assigned the material above the one you deleted.
- Move body up so that the wheels sit on the origin of the 3D view, I recommend using the side view using Numpad 3 for lining this up properly
- With body selected, hover over the viewport and press Ctrl + A, then select Location. This will apply the move action you just did.
- Export to fbx, all default settings

<img width="1687" height="673" alt="Screenshot_20251030_201835" src="https://github.com/user-attachments/assets/13d9854c-d885-46c6-a000-2d255b9b8ade" />

Reload the backup again and export the main model:
- Delete tire_fl, tire_fr, tire_rl and tire_rr
- Duplicate all parts you would like deformation for (body is required here, but steering_wheel_lo, shocks, wheelhubs and the suspension will crash the game if they have deformation)
- Rename each part to have the part name with the "_crash" suffix
- Select Add -> Lattice, move it to 0 on all axes, scale and move it to encompass the car model
- Go to the lattice's Data tab, set all 3 axes of resolution to 10 and tick Outside
- Select all crash models, then make sure that body_crash is the main selected object (the one with its data shown in the right side), press Shift+H to hide all objects but them
- Go to the Modifiers tab, select Add Modifier, select Deform -> Lattice, then under the Object dropdown select Lattice
- From the modifier's small dropdown menu, select Copy to Selected to apply the changes to every crash model

<img width="364" height="575" alt="Screenshot_20251030_195908" src="https://github.com/user-attachments/assets/f1e6af40-f627-4d78-a177-a51d936b36a1" />

- Select the lattice, enter Edit Mode, enable Proportional Editing in the top center list of options, then in the dropdown next to it set Proportional Size to 0.01m

<img width="365" height="341" alt="Screenshot_20251030_202022" src="https://github.com/user-attachments/assets/ffc7a079-a7ab-4df3-9fa0-bad1b0a47f6c" />

- Move the lattice's vertices until the car deforms how you'd like it to
- Export to fbx, all default settings

<img width="1045" height="647" alt="Screenshot_20251030_200116" src="https://github.com/user-attachments/assets/959b8c15-37b6-4aea-a9ca-eb420fe4499a" />

All 3 .fbx files can now be imported using the `-create_fouc_bgm` parameter in my W32/BGM tool, with the main model being body.bgm and crash.dat, tires being tire.bgm, and the menu model being menucar_xx.bgm

Car collisions are stored in `body.ini` and can be easily done as follows:
- Run the W32/BGM tool on the main model's resulting bgm file with `-export_text`
- Search for `vAABBMin` in the resulting .txt file, find the one corresponding to `body`
- Insert the min and max values into this sample file, save it as body.ini (I recommend changing the second value of Min to 0.1 for better interaction with curbs):
```
CollisionFullMin     = { -0.8648945, 0.1, -1.8625445 }
CollisionFullMax     = { 0.865505, 1.1911374, 2.1228676 }

CollisionBottomMin     = CollisionFullMin
CollisionBottomMax     = CollisionFullMax

CollisionTopMin         = CollisionFullMin
CollisionTopMax         = CollisionFullMax
```

Normal maps are stored in a different format in FOUC, here's a quick set of commands to convert regular ones to its format, using bash and imagemagick  
Run these commands with bash in a folder containing only the normal maps in .dds format.
```
for f in *.dds; do convert "$f" -channel B -evaluate set 0% "$f"; done
for f in *.dds; do convert "$f" -channel A -evaluate set 100% -define dds:compression=dxt5 "$f"; done
for f in *.dds; do convert "$f" -separate -swap 0,3 -combine "$f"; done
for f in *.dds; do convert "$f" -channel R -evaluate set 0% "$f"; done
```

Empty normals, speculars, lights and a sample windows.dds
The game will crash when the car loads in the menu if you don't have most of these, so this is needed if you don't have any normals, lights_glow or other such textures
https://drive.google.com/file/d/1hQPyPWKuZhmpJFLX5c_RH_ebxh-xTHzj/view?usp=sharing

EXTRA NOTE: The reflectivity of the light shader depends on the alpha value of lights_glow, lights_glowlit and lights_damaged_glow
If the texture looks too dark, simply decrease the alpha value of those textures, 0 alpha makes the lights show up matte, near-identically to how the car diffuse shader looks
Make sure to keep the alpha channel identical between lights_glow and lights_glowlit, otherwise shading on the rest of the lights may change when you brake or reverse!

<img width="688" height="360" alt="image" src="https://github.com/user-attachments/assets/b53e2de1-826b-407a-b06a-155f8376187e" />
