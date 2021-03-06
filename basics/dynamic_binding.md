# Dynamic Binding

## Dynamic binding

Jolie allows output ports to be dynamically bound, i.e., their locations and protocols \(called _binding informations_\) can change at runtime. Changes to the binding information of an output port is local to a behaviour instance: output ports are considered part of the local state of each instance. Dynamic binding is obtained by treating output ports as variables. For instance, the following would print the location and protocol name of output port `Printer`:

```text
// Printer.iol
interface PrinterInterface {
    OneWay: printText( string )
}

//dynamic_binding_example.ol

include "console.iol"
include "Printer.iol"

outputPort P {
    Location: "socket://p:80"
    Protocol: sodep
    Interface: PrinterInterface
}

main
{
    println@Console( P.location )();
    println@Console( P.protocol )()
}
```

Binding information may be entered at runtime by making simple assignments:

```text
include "Printer.iol"

outputPort P {
    Interfaces: PrinterInterface
}

main
{
    P.location = "socket://p:80/";
    P.protocol = "sodep"
}
```

## The binding registry example

We show a usage example of dynamic binding and binding transmission by implementing a binding registry, i.e., a service that shares binding information. The registry offers a request-response operation, `getBinding`, that returns the binding information for contacting a service. We identify service by simple names. The interface of the registry is thus:

```text
interface RIf {
    RequestResponse: getBinding( string )( Binding )
}
```

where `Binding` is the type of port bindings defined in the standard Jolie library. Below we implement the registry behaviour, which supplies binding information for an inkjet printer and a laser printer \(whose services we leave unspecified\).

```text
main
{
    getBinding( name )( b ){
        if ( name == "LaserPrinter" ){
            b.location = "socket://p1.com:80/";
            b.protocol = "sodep"
        } else if ( name == "InkJetPrinter" ) {
            b.location = "socket://p2.it:80/";
            b.protocol = "soap"
        }
    }
}
```

Finally, we define a client that calls `getBinding` for discovering the laser printer:

```text
outputPort Registry {
    // omitted
}

outputPort Printer {
    Interfaces: PrinterInterface
}

main
{
    getBinding@Registry( "LaserPrinter" )( Printer );
    printText@Printer( "My text" )
}
```

