/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/

package model;

import java.util.Map;

/**
 * Creates an ATV.
 * @author Zachariah Wingo
 * @version 1.0
 */
public class Atv extends AbstractVehicle {

    /** Death Time. */
    private static final int DEATH_TIME = 15;
    
    /**
     * Constructs an ATV.
     * @param theX is the starting X coordinate.
     * @param theY is the starting Y coordinate.
     * @param theDir the starting direction.
     */
    public Atv(final int theX, final int theY, final Direction theDir) {
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
        boolean canPass;
        
        if (theTerrain == Terrain.WALL) {
            canPass = false;
        } else {
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
        Direction direction = Direction.random();
        
        while (theNeighbors.get(direction) == Terrain.WALL) {
            direction = Direction.random();
        }
        
        return Direction.random();
    }

}
