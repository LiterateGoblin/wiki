---
title: GIMP ToolKit (GTK)
---
GIMP ToolKit - typically referred to as simply GTK - is a graphical user interface framework. It is compatible with Windows, Mac OS, and Linux. Written in C, it features language bindings to support writing GTK and other languages, such as Rust. It is heavily based around the object oriented programming paradigm.

It was named GIMP ToolKit to remember the application it was original developed for: GIMP.

## GTK4

The components that make up a GTK4 application are known as *widgets.* All widgets descend from the `Widget` type, which in turn descend from the `GObject` type in the class hierarchy. Each component is capable of listening to *signals* - events that trigger a callback when received. Custom signals can be defined to send and receive.

GTK is built using one event loop that is responsible for checking is signals have been received and running the callback if one has. Thus, it is advised that callbacks that start operations that will be long-running should do so in a separate thread. This avoids blocking the graphical user interface thread, which "freezes" when blocked.

`GObjects` are not thread-safe.

### Concepts

#### Expressions

An expression (in the GTK sense) is a way to assign a value to a reference - even one that is several steps away. For example, given two objects named `object1` and `object2`, an expression could refer to the property "A" of one (`object1.A`) and itself be assigned to a property of "two" `object2.prop`. The expression need not refer to a value that exists until it is evaluated, for example, the expression mapping to `object1.A` can be assigned to `object2.prop` before `object1` has been created.

The following code binds `list_item->item->number` to a `label->label`  in Rust:

```
let label = Label::new(None);
...
list_item
    .property_expression("item")
    .chain_property::<IntegerObject>("number")
    .bind(&label, "label", Widget::NONE);
```

Expressions cannot handle bidirectional relationships.

#### Composite Templates

A GTK interface can be described using an XML document to separate the interface design from the logic. A pair of `<interface>` tags are required as the outermost tags. Each tag can describe a GTK widget or its properties, and generally has the file extensions `.ui`. Then, as a build step the templates are processed according to another XML document called `resources.gresource.xml`.

### GTK4 and Rust

GTK4 features Rust bindings. However, due to differences between C and Rust, special procedures need to taken when writing GTK code in Rust. These include, but are not limited to:

- subclassing is done by ensuring that a struct implements all the necessary traits and interfaces of each type that it is descended from.  Two structs need to be created when subclassing - a wrapper struct that is external and has new behaviors, and an implementation struct that has any overridden behaviors
- callbacks that mutate state must do so using a type that allows for interior mutability, such as a `std::cell::Cell`

## References

 1. <https://www.gtk.org/about/>. Accessed 2023-11-24
 2. <https://www.gtk.org/docs/getting-started/>. Accessed 2023-11-24
 3. <https://www.gtk.org/docs/installations/windows/>. Accessed 2023-11-24
 4. <https://gtk-rs.org/gtk4-rs/git/book/widgets.html>. Accessed 2023-11-24
 5. <https://gtk-rs.org/gtk4-rs/git/book/g_object_subclassing.html>. Accessed 2023-11-24
 6. <https://gtk-rs.org/gtk4-rs/git/book/g_object_signals.html>. Accessed 2023-11-24
 7. <https://gtk-rs.org/gtk4-rs/git/book/main_event_loop.html>. Accessed 2023-11-24
 8. <https://gtk-rs.org/gtk4-rs/git/book/list_widgets.html>. Accessed 2023-11-26
 9. <https://gtk-rs.org/gtk4-rs/stable/latest/docs/gtk4/struct.Expression.html>. Accessed 2023-11-26
10. <https://gtk-rs.org/gtk4-rs/git/book/composite_templates.html>. Accessed 2023-11-26
11. [https://gtk-rs.org/gtk4-rs/git/book/todo_1.html](https://gtk-rs.org/gtk4-rs/git/book/todo_1.html#task-row). Accessed 2023-11-26
