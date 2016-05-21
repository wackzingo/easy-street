/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/

package model;

import java.util.Map;

/**
 * Creates a bicycle that can travel on roads and trails.
 * @author Zachariah Wingo
 * @version 1.0
 */
public class Bicycle extends AbstractVehicle {
    
    /** Death Time. */
    private static final int DEATH_TIME = 25;
    
    /**
     * Constructs a bicycle.
     * @param theX starting x coordinate.
     * @param theY starting y coordinate.
     * @param theDir starting direction.
     */
    public Bicycle(final int theX, final int theY, final Direction theDir) {
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
            || theTerrain == Terrain.TRAIL
            || (theTerrain == Terrain.LIGHT && theLight == Light.GREEN)) {
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

        // Makes coding much easier
        final Terrain tAhead = theNeighbors.get(getDirection());
        final Terrain tLeft = theNeighbors.get(getDirection().left());
        final Terrain tRight = theNeighbors.get(getDirection().right());

        if (tAhead == Terrain.TRAIL) {
            direction = getDirection();
        } else if (tLeft == Terrain.TRAIL) {
            direction = getDirection().left();
        } else if (tRight == Terrain.TRAIL) {
            direction = getDirection().right();
        } else if (tAhead == Terrain.STREET || tAhead == Terrain.LIGHT) {
            direction = getDirection();
        } else {
            
            if (tLeft == Terrain.STREET) {
                direction = getDirection().left();
            } else if (tRight == Terrain.STREET) {
                direction = getDirection().right();
            } else {
                direction = getDirection().reverse();
            }
        }

        return direction;
    }

}
