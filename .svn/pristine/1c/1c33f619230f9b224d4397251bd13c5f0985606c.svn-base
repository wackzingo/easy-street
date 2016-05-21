/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/

package model;

import java.util.Map;

/**
 * Creates a Truck vehicle.
 * 
 * @author Zachariah Wingo
 * @version 1.0
 */
public class Truck extends AbstractVehicle {

    /** Death Time. */
    private static final int DEATH_TIME = 0;
    
    /**
     * Constructs a Truck.
     * 
     * @param theX initial starting x coordinate.
     * @param theY initial starting y coordinate.
     * @param theDir initial starting direction.
     */
    public Truck(final int theX, final int theY, final Direction theDir) {
        super(theX, theY, theDir, DEATH_TIME);
    }

    /**
     * Check to see if a vehicle can pass on the given terrain.
     * 
     * @param theTerrain the terrain to check.
     * @param theLight the color of the light.
     */
    @Override
    public boolean canPass(final Terrain theTerrain, final Light theLight) {
        boolean canPass = false;
        
        if (theTerrain == Terrain.STREET 
            || (theTerrain == Terrain.LIGHT)) {

            canPass = true;
        }

        return canPass;
    }
    
    /**
     * Chooses a direction for the vehicle to travel.
     * 
     * @param theNeighbors is a Map of the terrain surrounding the vehicles current position.
     */
    @Override
    public Direction chooseDirection(final Map<Direction, Terrain> theNeighbors) {
      
        Direction direction;
        
        // Makes coding much easier.
        final Terrain tAhead = theNeighbors.get(getDirection());
        final Terrain tLeft = theNeighbors.get(getDirection().left());
        final Terrain tRight = theNeighbors.get(getDirection().right());
        
        // If there is an available terrain to pass on either left, right, or in-front
        // we will keep choosing random directions until we find an acceptable move.
        if (canPass(tAhead, Light.GREEN)
                        || canPass(tLeft, Light.GREEN) || canPass(tRight, Light.GREEN)) {

            // Sets a random direction. 
            direction = Direction.random();

            // Keep selecting a random direction until we get a valid move that is not reverse.
            while (direction == getDirection().reverse() 
                            || !canPass(theNeighbors.get(direction), Light.GREEN)) {
                
                direction = Direction.random();
            }

        } else {
            
            // We should only get here if there was no possible moves so go in reverse.
            direction = getDirection().reverse();
        }
        return direction;
    }
}
