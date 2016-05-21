/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/
package model;

/**
 * Creates a Taxi as a type of car.
 * @author Zachariah Wingo
 * @version 1.0
 *
 */
public class Taxi extends Car {

    /** The number of iterations the Taxi will wait at a red light before moving. */
    private static final int WAIT_FOR_LIGHT = 3;
    
    /** Count for the number of iterations waited. */
    private int myWaitCount;
    
    /**
     * Constructs a Taxi vehicle.
     * @param theX the initial starting x coordinate.
     * @param theY the initial starting y coordinate.
     * @param theDir the initial starting direction.
     */
    public Taxi(final int theX, final int theY, final Direction theDir) {
        super(theX, theY, theDir);
        myWaitCount = 0;
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
        
        if (theTerrain == Terrain.STREET  || (theTerrain == Terrain.LIGHT 
            && (theLight == Light.GREEN || theLight == Light.YELLOW
            || myWaitCount == WAIT_FOR_LIGHT))) {
            
            myWaitCount = 0;
            canPass = true;
            
        } else if (theTerrain == Terrain.STREET 
                        || (theTerrain == Terrain.LIGHT 
                        && (theLight == Light.RED && myWaitCount < WAIT_FOR_LIGHT))) {
            
            // If we can't move because the light is red and we have not waited
            // long enough then we will increment the myWaitCount and return false.
            myWaitCount++;
            
            canPass = false;
        }

        return canPass;
    }
    
    
}
