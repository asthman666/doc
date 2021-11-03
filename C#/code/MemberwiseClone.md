    Microsoft (R) Roslyn C# Compiler version 2.10.0.0
    Loading context from 'CSharpInteractive.rsp'.
    Type "#help" for more information.
    > var a = "str";
    > var b = a;
    > a.GetHashCode()
    -419715239
    > b.GetHashCode()
    -419715239
    > var c = string.Copy(a);
    > c.GetHashCode()
    -419715239
    > c = "strc";
    > c
    "strc"
    > c.GetHashCode()
    392608638
    > a.GetHashCode()
    -419715239

Consider this:

    > public class Person
    . {
    .     string name;
    .     public Person ShallowCopy() {
    .         return (Person)this.MemberwiseClone();
    .     }
    . }
    > var p1 = new Person();
    > p1.GetHashCode()
    59652943
    > var p2 = p1.ShallowCopy();
    > p2.GetHashCode()
    62676156
    > 

If you call MemberwiseClone, you'll end up with two separate instances of Person, but their name variables, while distinct, will have the same value - they'll refer to the same string instance. This is because it's a shallow clone.

If you change the name in one of those instances, that won't affect the other, because the two variables themselves are separate - you're just changing the value of one of them to refer to a different string.    