# Kotlin-Inheritance-Example
Program that implements classes for different kinds of dwellings. Shows how to: Create class hierarchy, variables and functions with inheritance, abstract class, overriding, and private vs. public variables.

```kotlin
import kotlin.math.PI
import kotlin.math.sqrt

/**
 * Program that implements classes for different kinds of dwellings.
 * Shows how to:
 * Create class hierarchy, variables and functions with inheritance,
 * abstract class, overriding, and private vs. public variables.
 */

fun main() {

    val squareCabin = SquareCabin(6, 50.0)
    val roundHut = RoundHut(3, 10.0)
    val roundTower = RoundTower(4, 15.5)

    with(squareCabin) {
        println("\nSquare Cabin\n============")
        println("Capacity: $capacity")
        println("Material: $buildingMaterial")
        println("Has room? ${hasRoom()}")
//        println("Floor area: ${floorArea()}")
        // For the area values, it would be a nicer user experience
        // to only show a couple of decimal places.
        println("Floor area: %.2f".format(floorArea()))

    }

    with(roundHut) {
        println("\nRound Hut\n=========")
        println("Material: $buildingMaterial")
        println("Capacity: $capacity")
        println("Has room? ${hasRoom()}")
        println("Floor area: %.2f".format(floorArea()))

        /*
        * Note: This is an example of why inheritance is so powerful.
        * You can call the getRoom() function on all the subclasses of Dwelling
        * without additional code in those classes.
        * */

        println("Has room? ${hasRoom()}")
        getRoom()
        println("Has room? ${hasRoom()}")
        getRoom()

        println("Carpet size: ${calculateMaxCarpetSize()}")
    }

    with(roundTower) {
        println("\nRound Tower\n==========")
        println("Material: $buildingMaterial")
        println("Capacity: $capacity")
        println("Has room? ${hasRoom()}")
        println("Floor area: %.2f".format(floorArea()))

        println("Carpet size: ${calculateMaxCarpetSize()}")
    }
}


abstract class Dwelling(private var residents: Int) {

    abstract val buildingMaterial: String
    abstract val capacity: Int

    fun hasRoom(): Boolean {
        return residents < capacity
    }

    fun getRoom() {
        if (capacity > residents) {
            residents++
            println("You got a room!")
        } else {
            println("Sorry, at capacity and no rooms left.")
        }
    }

    abstract fun floorArea(): Double
}


class SquareCabin(residents: Int,
                  private val length: Double) : Dwelling(residents) {

    override val buildingMaterial = "Wood"
    override val capacity = 6

    override fun floorArea(): Double {
        return length * length
    }
}


open class RoundHut(
    residents: Int,
    private val radius: Double) : Dwelling(residents) {

    override val buildingMaterial = "Straw"
    override val capacity = 4

    override fun floorArea(): Double {
        return PI * radius * radius
    }

    fun calculateMaxCarpetSize(): Double {
        val diameter = 2 * radius
        return sqrt(diameter * diameter / 2)
    }
}

/*
*
If you omit val or var in in a constructor,
* then the only places that can access these parameters
* are initialization statements that are
* evaluated at construction time.
* This is useful when you want to do something
* with a value "before storing it"
* */
class RoundTower(residents: Int, radius: Double,
                 private val floors: Int = 2) : RoundHut(residents, radius) {

    override val buildingMaterial = "Stone"
    override val capacity = 4 * floors

    override fun floorArea(): Double {
        return super.floorArea() * floors
    }
}

/*
* Summary
In this codelab you learned how to:

    Create a class hierarchy, that is a tree of classes where children inherit functionality from parent classes. Properties and functions are inherited by subclasses.
    Create an abstract class where some functionality is left to be implemented by its subclasses. An abstract class can therefore not be instantiated.
    Create subclasses of an abstract class.
    Use override keyword to override properties and functions in subclasses.
    Use the super keyword to reference functions and properties in the parent class.
    Make a class open so that it can be subclassed.
    Make a property private, so it can only be used inside the class.
    Use the with construct to make multiple calls on the same object instance.
    Import functionality from the kotlin.math library
* */
```
