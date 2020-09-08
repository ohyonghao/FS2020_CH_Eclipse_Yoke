# FS2020 CH Eclipse Yoke Custom Script
Configuration mappings for the CH Products Eclipse Yoke to work with FS2020 better.

# Installation
1. First install the CH Product Control Manager. 

2. Open the CH Control Manager and create a custom map, be sure to enable CMS scripting.

3. Open the CMS Script Editor and insert the ElevatorTrim.cms file.

4. Exit the CMS Script Editor

5. Go to the CMS Control tab.

6. Click on Axis A1

7. Make sure it is mapped as DirectX, and change the Device to your Eclipse Yoke

8. Set the Axis to Slider 0 (S0).

9. "Download" the script to the Yoke. This really should be called upload as it uploads the scirpt to the yoke.

10. Test it by using the Test/Calibrate dialog. Moving the vertical scroll wheel on the yoke itself, not the one on the body,
you should see S0 start from a centered position with value 128 and increment up.

11. If this is too jerky for your taste, go back into the CMS Script Editor and change the step definition.

# Further Updates

Part of this is learning from the very slim material available about the capabilities of this system. The system
isn't very well setup for good code organization. It appears so far that everything runs in a single event loop.
The timing of this loop isn't apparent, whether it runs at a set rate per second, or just as fast as it can.

Organization will probably change. I'm in the process of understanding how this should be organized. It looks to be
that it may need to be organized by game. The CH Control Panel allows for changing scripts easily. If that is the 
case I may write a script combiner to allow for modular code structure, most likely using python.

# Best Practices

Here is where feedback is needed and ideas in the bug section. Feel free to start a discussion.

## Script Organization

* Independent button presses need to be guarded by `SEQUENCE` blocks for updating button state or actions.
* Initialization should go above the relavent block or section. In this regard the elevator trim should start
with a line to initialize the elevator trim guarded by a conditional statement `IF( FIRSTSCAN ) THEN`, and ending
with an `ENDIF`.
* Use a comment block with a line of asterisks to begin a section.

# Potential Problems

This language appears to be organized with an explicit memory allocation structure similar to registers in the CPU.
Essentially you have two types of registers, bit variables and analog variables. Bit variables are booleans, and analog
variables are perhaps floating point or integer. More experimentation and reading will need to be done on this aspect,
but as currently understood we create these using B# and A# respectively, such as `B1` for the first boolean value, and
`A1` for the first analog value. If this is the case then combining scripts will be a bit more painful.

# License

This is licensed under the GNU 3.0 license, see the `LICENSE` file for more details.

# Contributions

Please fork this repository and create a pull request.
