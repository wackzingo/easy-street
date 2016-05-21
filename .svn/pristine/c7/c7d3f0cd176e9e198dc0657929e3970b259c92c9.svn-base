/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/

package model;

import java.util.Map;

/**
 * Creates a human vehicle.
 * @author Zachariah Wingo
 * @version 1.0
 */
public class Human extends AbstractVehicle {
    
    /** Death Time. */
    private static final int DEATH_TIME = 45;
    
    /** The terrain the vehicles starts on. */
    private final Terrain myInitialTerrain;
    
    /**
     * Constructs a human.
     * @param theX initial starting x coordinate.
     * @param theY initial starting y coordinate.
     * @param theDir initial starting direction.
     * @param theTerrain initial starting terrain.
     */
    public Human(final int theX, final int theY, 
                 final Direction theDir, final Terrain theTerrain) {
        
        super(theX, theY, theDir, DEATH_TIME);
        
        myInitialTerrain = theTerrain;
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
        
        if (theTerrain == myInitialTerrain) {
            canPass = true;
        } else if (myInitialTerrain == Terrain.STREET && theTerrain == Terrain.LIGHT) {
            canPass = true;
        } else if (myInitialTerrain == Terrain.LIGHT && theTerrain == Terrain.STREET) {
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
     
        // Keep selecting a random direction until we get a valid move that is not reverse
        while (!canPass(theNeighbors.get(direction), Light.RED)) {
            direction = Direction.random();
        }
        
        return direction;
    }
}
