/*
* TCSS 305 – Winter 2016
* Assignment 3 – EasyStreet
*/
package model;

import java.util.Map;

/**
 * Creates a vehicle.
 * @author Zachariah Wingo
 * @version 1.0
 */
public abstract class AbstractVehicle implements Vehicle {
    
    /** The direction. */
    private Direction myDirection;
    
    /** The current x position. */
    private int myX;
    
    /** The current y position. */
    private int myY;
    
    /** The initial starting x position. */
    private final int myInitialX;
    
    /** The initial starting y position. */
    private final int myInitialY;
    
    /** The initial direction. */
    private final Direction myInitialDirection;
    
    /** Vehicle alive status. */
    private boolean myAliveStatus;
    
    /** Counts pokes to track death status. */
    private int myPokes;
    
    /** Death Time. */
    private int myDeathTime;
    
    /**
     * Creates a vehicle.
     * @param theX the starting x coordinate.
     * @param theY the starting y coordinate.
     * @param theDir the starting direction.
     * @param theDeathTime the time vehicle is dead.
     */
    public AbstractVehicle(final int theX, final int theY, final Direction theDir,
                           final int theDeathTime) {
        
        // Vehicles should always start alive.
        myAliveStatus = true;
            
        // Pokes should always start at zero.
        myPokes = 0;
        
        // Set starting x.
        setX(theX);
        myInitialX = theX;
        
        // Set starting y.
        setY(theY);
        myInitialY = theY;
        
        // Set initial starting direction.
        myInitialDirection = theDir;
        
        // Set initial direction.
        setDirection(theDir);
        
        // Set death time.
        setDeathTime(theDeathTime);
    }
    
    /**
     * Determines what happens when vehicles collide.
     * 
     * @param theOther represents the vehicle that collides with this vehicle.
     */
    @Override
    public final void collide(final Vehicle theOther) {
        
        if (isAlive() && theOther.isAlive() && myDeathTime > theOther.getDeathTime()) {
            myAliveStatus = false;
        }
    }
    
    /**
     * Determines if a vehicle can pass. This should be overridden.
     * 
     * @param theTerrain is the type of terrain being evaluated.
     * @param theLight is the color of the light.
     */
    @Override
    public boolean canPass(final Terrain theTerrain, final Light theLight) {
        
        return theTerrain == Terrain.STREET && theLight == Light.GREEN;
    }
    
    /**
     * Chooses a direction.
     * 
     * @param theNeighbors is a map of the terrain types surrounding the vehicle.
     */
    @Override
    public Direction chooseDirection(final Map<Direction, Terrain> theNeighbors) {
        return Direction.random();
    }

    /**
     * Sets the death time of the vehicle.
     * 
     * @param theDeathTime represents the number of iterations a vehicle stays dead.
     */
    public final void setDeathTime(final int theDeathTime) {
        myDeathTime = theDeathTime;
    }
    
    /**
     * @return returns the death time of the vehicle as an int.
     */
    @Override
    public final int getDeathTime() {
        return myDeathTime;
    }

    /**
     * Returns the filename of the image.
     * 
     * @return returns image of a dead/alive vehicle.
     */
    @Override
    public final String getImageFileName() {
        
        // Filename of a vehicle that is alive.
        final String alive = getClass().getSimpleName().toLowerCase() + ".gif";
        
        // Filename of a vehicle that is dead.
        final String dead = getClass().getSimpleName().toLowerCase() + "_dead.gif";
        
        // Ternary operator (conditional) ? value_if_true : value_if_false;
        return (isAlive()) ? alive : dead;
    }

    /**
     * Returns the current direction of the vehicle.
     * 
     * @return returns the current direction of the vehicle as a Direction.
     */
    @Override
    public final Direction getDirection() {
        return myDirection;
    }

    /**
     *  Returns the current X coordinate.
     *  
     *  @return the current X coordinate as an integer.
     */
    @Override
    public final int getX() {
        return myX;
    }

    /**
     * Returns the current Y coordinate.
     * 
     * @return returns current Y coordinate as an integer.
     */
    @Override
    public final int getY() {
        return myY;
    }

    /**
     * Returns the status of the vehicles alive status.
     * 
     * @return returns true if vehicle is alive and false if dead.
     */
    @Override
    public final boolean isAlive() {
        return myAliveStatus;
    }

    /**
     * Pokes vehicle every iteration when dead and serves as a counter for the death timer.
     */
    @Override
    public final void poke() {

        if (myPokes == myDeathTime) {
            myAliveStatus = true;
            myPokes = 0;
        } else {
            myPokes++;
        }
        
    }

    /**
     * Resets vehicle to original starting x coordinate, y coordinate, and direction.
     * The pokes gets reset to 0 and the alive status is set to true.
     */
    @Override
    public final void reset() {
        setX(myInitialX);
        setY(myInitialY);
        setDirection(myInitialDirection);
        myPokes = 0;
        myAliveStatus = true;
    }

    /**
     * Sets the Direction.
     * 
     * @param theDir is the current direction of the vehicle.
     */
    @Override
    public final void setDirection(final Direction theDir) {
        myDirection = theDir;
    }

    /**
     *  Sets the X coordinate.
     *  
     *  @param theX is current x coordinate.
     */
    @Override
    public final void setX(final int theX) {
        myX = theX;
    }

    /**
     * Sets the initial starting Y coordinate.
     * 
     * @param theY is the initial y coordinate.
     */
    @Override
    public final void setY(final int theY) {
        myY = theY;
    }

    @Override
    public String toString() {
        
        final StringBuilder sb = new StringBuilder(160);
        
        sb.append("Vehicle: ");
        sb.append(getClass().getSimpleName().toLowerCase());
        sb.append(", Alive: ");
        sb.append(isAlive());
        sb.append(", Pokes: ");
        sb.append(myPokes);
        
        return sb.toString();
    }
}
