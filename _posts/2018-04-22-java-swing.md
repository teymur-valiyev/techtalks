Swing The Model View Controller

* Model The model encompasses the state data for each component. There are different models for different types of components. For example, the model of a scrollbar component might contain information about the current position of its adjustable "thumb," its minimum and maximum values, and the thumb's width (relative to the range of values). A menu, on the other hand, may simply contain a list of the menu items the user can select from. This information remains the same no matter how the component is painted on the screen; model data is always independent of the component's visual representation.

* View The view refers to how you see the component on the screen. For a good example of how views can differ, look at an application window on two different GUI platforms. Almost all window frames have a title bar spanning the top of the window. However, the title bar may have a close box on the left side (like the Mac OS platform), or it may have the close box on the right side (as in the Windows platform). These are examples of different types of views for the same window object.

* Controller The controller is the portion of the user interface that dictates how the component interacts with events. Events come in many forms e.g., a mouse click, gaining or losing focus, a keyboard event that triggers a specific menu command, or even a directive to repaint part of the screen. The controller decides how each component reacts to the eventif it reacts at all.

## MVC in Swing

Swing actually uses a simplified variant of the MVC design called the model-delegate.
This design combines the view and the controller object into a single element, the UI delegate, which draws the component to the screen and handles GUI events


## Internal Frame

Same functions as a normal Frame object, but confined to the visible area of the container it is placed in

## Actions

Swing containers, such as JMenu, JPopupMenu, and JToolBar, can each accept action
objects with their add( ) methods. When an action is added, these containers automatically
create a GUI component, which the add( ) method then returns to you for customization.

For example, a JMenu or a JPopupMenu creates and returns a JMenuItem from an Action
while a JToolBar creates and returns a JButton. The action is then paired with the newly
created GUI component in two ways: the GUI component registers as a
PropertyChangeListener for any property changes that might occur in the action object,
while the action object registers as an ActionListener on the GUI component. Figure 3-1
shows the interactions between a menu item or toolbar and an Action.

Essentially, this means that if the menu item or button is selected by the user, the functionality inside the action is invoked. On the other hand, if the action is disabled, it sends a PropertyChangeEvent to both the menu item and the toolbar, causing them to disable and turn gray. Similarly, if the action's icon or name is changed, the menu and toolbar are automatically updated.


## The Action Interface
An action is defined by the interface it implements, in this case javax.swing.Action.
Action extends the ActionListener interface from AWT; this forces concrete classes
that implement Action to provide an actionPerformed( ) method. The programmer
uses the actionPerformed( ) method to implement whatever behavior is desired. For
example, if you are creating a Save action, you should put the code that saves the data inside of your actionPerformed( ) method.


## Events
Objects implementing the Action interface must fire a PropertyChangeEvent when any
keyed property is changed, or when the action is enabled or disabled. Containers that accept actions typically listen for these PropertyChangeEvent notifications so they can update their own properties or appearances.
public abstract void addPropertyChangeListener(PropertyChangeListener listener)
public abstract void removePropertyChangeListener(PropertyChangeListener listener)
Add or remove the specified PropertyChangeListener from the event listener list

## The AbstractAction Class
The AbstractAction class is an abstract implementation of the Action interface.
AbstractAction provides the default functionality for almost all methods in the Action
interface.

## Graphical Interface Events

Whenever you interact with your application's user interface, the application receives an event
from the windowing system to let it know that something happened. Some events come from
the mouse, such as mouse clicks, mouse movements, and mouse drags


## Graphics Environments

You can retrieve that information for your own code through the GraphicsEnvironment, GraphicsDevice,
and GraphicsConfiguration classes from the java.awt package. While they aren't
part of Swing proper, these classes are definitely useful for Swing applications, especially
those that take full advantage of their environment.
To sum up these classes, a system keeps a local GraphicsEnvironment object that
describes the devices on the system with an array of GraphicsDevice objects. Each
GraphicsDevice contains (or at least may contain) multiple configurations of device
capabilities (such as pixel formats or which visual screen you're on) bundled up in an array of
GraphicsConfiguration objects.

## Headless Modes
One other variation on the graphics environment is "headless" operation. This mode of running
without any monitor shows up quite often on back-end systems. Java servlets trying to use the
AWT, 2D, and Swing classes to draw dynamic graphs for a web page are a classic example of
applications that need a graphics environment on a machine that might not have any graphics
displays. You can detect such a case with the GraphicsEnvironment.isHeadless( )
call

## Sending Change Events in Swing
Swing uses two different change event classes. The first is the standard
java.beans.PropertyChangeEvent class. This class passes a reference to the
object, sending the change notification as well as the property name, its old value, and its new
value. The second, javax. swing.event.ChangeEvent, is a lighter version that
passes only a reference to the sending objectin other words, the name of the property that
changed, as well as the old and new values, are omitted.

## The JComponent Class
JComponent is an abstract class that almost all Swing components extend; it provides much
of the underlying functionality common throughout the Swing component library. Just as the
java.awt.Component class serves as the guiding framework for most of the AWT
components, the javax.swing.JComponent class serves an identical role for the Swing
components. We should note that the JComponent class extends java.awt.Container
(which in turn extends java.awt.Component), so it is accurate to say that Swing
components carry with them a great deal of AWT functionality as well.

Because JComponent extends Container, many Swing components can serve as
containers for other AWT and Swing components. These components may be added using the
traditional add( ) method of Container. In addition, they can be positioned with any Java
layout manager while inside the container. 

## Inherited Properties
Swing components carry with them several properties that can be accessed through
JComponent but otherwise originate with AWT. Before we go any further, we should review
those properties of java.awt.Container and java.awt.Component that can be used
to configure all Swing components. 

Let's discuss these properties briefly. The background and foreground properties
indicate which colors the component uses to paint itself. We should mention that with Swing the
background property is disabled if the component is transparent (not opaque). The readonly
colorModel property returns the current model used to translate colors to pixel values;
generally, the user does not need to access this property. The font property lets you get or
set the font used for displaying text in the component.
The indexed component property maintains a list of all the components inside the container.
You can tell how many there are with the integer componentCount property. If you want to
access all of them through a Component array, retrieve the components property. The
insets property specifies the current insets of the container, while the layout property
indicates which layout manager is managing the components of the container. Technically, this
means that you can use any component as a container. Don't be misled; if a component doesn't
seem like a reasonable container, it probably can't be used as one. (Don't, for example, try to
add a JButton to a JScrollBar.) A number of components use these properties for
internal, specialized layout managers and components.
The locale property specifies the internationalization locale for the application. The
location property indicates the x,y coordinates of the component's upper-left corner in the
container's coordinate space. If you want to see the location of the component's upper-left
corner in screen coordinates, use the read-only locationOnScreen property.
The name property gives this component a string-based name that components can display if
they choose. The parent property references the container that is acting as this component's
parent, or null if there is none. The size property specifies the component's current height
and width in pixels.
The showing property indicates whether the component is currently showing on the screen,
while the visible property tells if the component is marked to be drawn on the screen.
There's an odd, nonintuitive relationship between visible and showing. A component that
is visible isn't necessarily showing. "Visible" means that a component is capable of being
displayed; "showing" means that the component is actually displayed (though it may be
obscured by something else). Most containers (JPanel, JFrame, etc.) are invisible by
default; most other components (JButton, etc.) are visible by default. So if you add a
JButton to an invisible JFrame, for example, the button is visible but not showing. It can be
displayed but happens to be in a container that isn't currently displayed.
Finally, if the valid property is false, the component needs to be resized or moved by the
component's layout manager. If it is true, the component is ready to be displayed.




## UI Delegates and UIClassIDs

Each Swing component maintains a read-only string constant, UIClassID, that identifies the
type of UI delegate that it uses. Most Swing components override the accessor
getUIClassID( ) and return a string constant, typically the letters "UI" appended to the
name of the component (without the "J").

##  Adding Borders
It's easy to add borders to Swing components, a feature AWT lacks. The JComponent
border property accepts objects that implement the javax.swing.border.Border
interface.
JLabel label = new JLabel("A Simple Label");
label.setBorder(BorderFactory.createEtchedBorder( ));

## Working with Tooltips
JComponent also provides Swing components with support for tooltips. Tooltips are small
windows of text that pop up when the user rests the mouse over the target component. 

JButton button = new JButton("Press Me!"); // JButton extends JComponent.
button.setToolTipText("Go Ahead!");
System.out.println(button.getToolTipText( ));

## The JPanel Class
JPanel is an extension of JComponent (which, remember, extends
java.awt.Container) used for grouping together other components. It gets most of its
implementation from its superclasses. Typically, using JPanel amounts to instantiating it,
setting a layout manager (this can be set in the constructor and defaults to a FlowLayout),
and adding components to it using the add( ) methods inherited from Container.

## The JRootPane Class
JRootPane is a special container that extends JComponent and is used by many of the
other Swing containers. It's quite different from most containers you're probably used to using. The first thing to understand about JRootPane is that it contains a fixed set of components: aComponent called the glass pane and a JLayeredPane called, logically enough, the layered pane. Furthermore, the layered pane contains two more components: a JMenuBar and a Container called the content pane.

The glass pane
Hidden, by default. If you make the glass pane visible, then it's like a sheet of glass over all the other parts of the root pane. It's completely transparent unless you implement the glass pane's paintComponent method so that it does something, and it can intercept input events for the root pane. 

The layered pane
Serves to position its contents, which consist of the content pane and the optional menu bar. Can also hold other components in a specified Z order.

The content pane
The container of the root pane's visible components, excluding the menu bar. 

The optional menu bar
The home for the root pane's container's menus. If the container has a menu bar, you generally use the container's setJMenuBar method to put the menu bar in the appropriate place. 