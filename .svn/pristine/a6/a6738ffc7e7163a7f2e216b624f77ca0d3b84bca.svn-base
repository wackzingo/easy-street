/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/
package model;

import java.util.Map;

/**
 * Creates an car.
 * @author Zachariah Wingo
 * @version 1.0
 */
public class Car extends AbstractVehicle {
    
    /** Death Time. */
    private static final int DEATH_TIME = 5;
    

    /**
     * Constructs a car object.
     * 
     * @param theX sets the initial X value.
     * @param theY sets the initial Y value.
     * @param theDir sets the initial direction.
     */
    public Car(final int theX, final int theY, final Direction theDir) {
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
                        || (theTerrain == Terrain.LIGHT 
                            && (theLight == Light.GREEN || theLight == Light.YELLOW))) {

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
        
        if (tAhead == Terrain.STREET || tAhead == Terrain.LIGHT) {
            direction = getDirection();
        } else if (tLeft == Terrain.STREET || tLeft == Terrain.LIGHT) {
            direction = getDirection().left();
        } else if (tRight == Terrain.STREET || tRight == Terrain.LIGHT) {
            direction = getDirection().right();
        } else {
            direction = getDirection().reverse();
        }
        
        return direction;
    }


}
