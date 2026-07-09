# Circuits Intro and Parts Intro

## A (Very) Brief Circuit Overview (PART 1 VIDEO)

### Resistors

<insert images of pcbs with and without components>

Resistors are a component that limits current, and disperses that energy as heat. The basic equation for that is Ohm's Law, which is 

$$
V = IR
$$

This means, if you have a basic circuit such as this, 

![](assets/basic_resistor_circuit.png)

You can calculate the amperage `I` going through the resistor by using Ohm's law. The `V` in this case is the voltage across the resistor or the voltage difference between A and B. R is the resistance of 100 ohms, so your resulting amperage is 24/100 = 0.24A. 

For designing boards, the important thing to remember is that bare wire (our traces) also has resistance and this can cause problem for small electronics. You can see the equation in this image

![](assets/wire_resistivity.jpg)

The important thing to keep in mind here is that the area of a wire or trace is inversely proportional to its resistance. IE, the wider the wire the less resistance it has, and therefore it will limit current less. $\rho$ is a property of the material itself, so this is not something you need to worry about, other than knowing that $\rho$ increases slightly with heat.

TL;DR, if you expect a lot of current, which in this case we'll say is more than 0.1A, make the wires as wide as possible, so that they have the least amount of current.

#### In-video Quiz (Pause and calculate type of quiz):

What is the resistance of a circular wire of radius 1mm and length 1m. You have a $\rho$ value of 1 (HOW MANY MINUTES TO GIVE?, MAKE A TITLE CARD FOR THIS)

You have a battery of 24V. The battery has a trace with a square cross section of 0.1mm high and 1mm wide. The trace is 100m in length. How many amps are going through the wire? (HOW MANY MINUTES TO GIVE?, MAKE A TITLE CARD FOR THIS)

### Capacitors (DO I TRIM THIS DOWN? Do recruits need to know Q = CV or can I just go over actual use case equations [charging, discharging, RC, etc.?]) (maybe include video of charging and discharging on falstad/ltspice)

The next component of relevance is the capacitor. In basic terms, a capacitor is two plates of conductive metal with a voltage difference across them. 

![](assets/capacitor_diagram.png)

The voltage difference creates a force that pulls negative charges on one plate and positive charges on the other. This relationship is given by 

$$
Q = CV
$$

Where Q is the max charge on the capacitor at a voltage V, V is the voltage across the capacitor, usually because its been supplied that voltage by a battery, and C is the capacitance of the capacitor itself, this is a constant that is the main characteristic of a capacitor, and has the units of Farads.

In terms of use, a capacitor will draw or output whatever current it needs to reach or maintain a certain voltage across the plates.

We use capacitors to either stabilize a voltage from spikes or noise, and for this we can use specific capacitances to target specific bands of noise that we want to eliminate. We will discuss this in more depth later.

### Inductors

![](assets/inductor_diagram.png)

Inductors are the last of the three basic electrical components. Inductors convert electrical energy to magnetic energy, but the mechanisms by which it does that aren't relevant to us (Unless you want to make a motor). In actual use, inductors are what I would consider the opposite of a capacitor. They use voltage to keep a current stable. Inductors are any coil of wire or any circular flow of current, and these coils create magnetic fields. Basically, Inductors will vary their own voltage to maintain the present current flow.

### Diodes

Diodes are a special type of component that only allows current flow in one direction, but at the cost of a voltage drop (This is Vt, or the forward voltage of a diode). This drop is also a threshold that the voltage has to pass for current to flow at all. Their voltage drop varies slightly based on current, but often this is relatively constant and this also can be used for your circuit. 

![](assets/diodes_diagram.png)

There are several types of diodes with different use cases or unique characteristics that I will briefly go over now and in more depth later. 

Zener diodes have a forward voltage and a backward voltage, so while a voltage that exceeds the forward threshold allows current to flow as normal, there is a second negative threshold known as the backwards threshold that will allow current to pass in the reverse direction. 

A schottky diode has a low forward voltage and faster switching, for better efficiency, useful for when that is desired.

LEDs, or Light Emitting Diodes is a diode which also emits light, which is useful for indication and signaling information to the user.

Now lets see how diodes function in practice. Take this circuit for example.

![](assets/diodes_example.png)

This is a simple battery resistor diode setup, and you can see that the voltage of the battery is not constant. Let's say Vt is 0.7V, which is fairly standard for diodes. If our battery is at 0.5V, then no current will flow at all, because the diode's threshold has not been met. Let's now say that our battery is at 3V. Our current is equal to 3 - 0.7 = 2.3, divided by 1000 = 0.0023A, or 2.3mA. 

This is good math to know because a lot of components, including diodes, have a limit of how much current can flow through them safely without them exploding.

## Parts (PART 2 VIDEO)

There are three aspects to every part. A symbol generally represents what type of part it is. Diodes, Resistors, Inductors, Capacitors, all have their own symbols, and variations based on part variations. One schematic symbol can translate to a number of different packages for a part, which consists of size and footprint information of a part. 

![](assets/symbol_package_variant_diagram.png)

For example, you can see that an LED has these three (and more) different packages. And then that one specific packages has a number of different variants that differ in color, brightness, Vt (the diode voltage threshold), and how many amps they can take safely. So it's important to make sure that you spec your parts properly and build your circuit around the parts that you are speccing for.

Part selection is a very important part of the design process. This is where you'll decide the part's size, electrical properties, and the ports of your device. If you pick wrong, you may have to restart all of your work, or in the very worst case you find the problem only after manufacturing, in which case its irreversible.

### Integrated Circuit

The next type of component we're covering is the integrated circuit, or IC. ICs are small circuit chips that implement some predetermined functionality. All the necessary components are designed, tested, and put into a small chip package. 
The benefits of using ICs are that its really convenient to make a design very quickly. The problem is that each version of an IC has very specific operating values and sometimes its hard/expensive to find a chip that fits the exact parameters you need. Looking through datasheets can take a lot of time and effort.

![](assets/ic_diagram.png)

### Datasheets

On that note, let's talk about datasheets. Datasheets are maybe the most important part of designing PCBs. Datasheets tell you about an electrical component's specifications and characteristics. It tells you the component's capabilities, mechanical information (Package, recommended layout, and pin location), and electrical information. In terms of electrical information, some key things to look out for are maximum voltages and amperages, additional required components (common for ICs), schematic applications (sometimes it'll give you a full example schematic layout). Your datasheet will also give you reflow information and how the part will come to you (sometimes it's important to note the orientation of a part in its original packaging to tell which pin is which. This is important especially for small parts, which often don't have writing or it's too small to even acknowledge)

## Video section: go through a datasheet of current imu that tr uses (ISM SOMETHING) and find example layout and make a schematic based on it.

## Assignment: Design a charlieplexed led expansion for the Nucleo (Maybe Arduino). Use only through hole components. Give recruits the correct spacing of nucleo pins.

##### Notes to self:

When discussing speccing parts, talk about voltage/current limits for each type of component.

Insert curt videos at relevant points throughout this training.

https://www.youtube.com/playlist?list=PLLDpFymVGR_cEbovUed4v1fvSXxBGATA-
