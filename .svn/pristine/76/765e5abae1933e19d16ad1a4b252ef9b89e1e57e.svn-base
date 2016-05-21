/*
 * TCSS 305 - Easy Street
 */

package tests;

import static org.junit.Assert.*;

import java.util.HashMap;
import java.util.Map;

import model.Direction;
import model.Truck;
import model.Light;
import model.Terrain;

import org.junit.Test;

/**
 * Unit tests for class Truck.
 * 
 * @author Alan Fowler (acfowler@uw.edu)
 * @author Charles Bryan
 * @author Zachariah Wingo (wingoz@uw.edu)
 * @version Spring 2015
 */
public class TruckTest {

    /**
     * The number of times to repeat a test to have a high probability that all
     * random possibilities have been explored.
     */
    private static final int TRIES_FOR_RANDOMNESS = 5000;
    
    /** Test method for Truck constructor. */
    @Test
    public void testTruckConstructor() {
        final Truck t = new Truck(10, 11, Direction.NORTH);
        
        assertEquals("Truck x coordinate not initialized correctly!", 10, t.getX());
        assertEquals("Truck y coordinate not initialized correctly!", 11, t.getY());
        assertEquals("Truck direction not initialized correctly!",
                     Direction.NORTH, t.getDirection());
        assertEquals("Truck death time not initialized correctly!", 0, t.getDeathTime());
        assertTrue("Truck isAlive() fails initially!", t.isAlive());
    }
    
    /** Test method for Truck setters. */
    @Test
    public void testTruckSetters() {
        final Truck t = new Truck(10, 11, Direction.NORTH);
        
        t.setX(12);
        assertEquals("Truck setX failed!", 12, t.getX());
        t.setY(13);
        assertEquals("Truck setY failed!", 13, t.getY());
        t.setDirection(Direction.NORTH);
        assertEquals("Truck setDirection failed!", Direction.NORTH, t.getDirection());
    }

    /**
     * Test method for {@link Truck#canPass(Terrain, Light)}.
     */
    @Test
    public void testCanPass() {
        // Start from each terrain type except WALL, Grass, Trail
        for (final Terrain testTerrain : Terrain.values()) {
            if (testTerrain != Terrain.WALL // Trucks do not start on Walls.
                && testTerrain != Terrain.GRASS // Trucks do not start on Grass
                && testTerrain != Terrain.TRAIL) { // Trucks do not start on Trails.
                final Truck truck = new Truck(0, 0, Direction.NORTH);
                // go to each terrain type
                for (final Terrain t : Terrain.values()) {
                    // try the test under each light condition
                    for (final Light l : Light.values()) {
                        if ((t == testTerrain)
                            || (t == Terrain.LIGHT && testTerrain == Terrain.STREET)
                            || (t == Terrain.STREET && testTerrain == Terrain.LIGHT)) {

                            assertTrue("Truck started on " + testTerrain
                                                       + " should be able to pass " + t
                                                       + ", with light " + l,
                                       truck.canPass(t, l));
                        } else {

                            assertFalse("Truck started on " + testTerrain
                                         + " should NOT be able to pass " + t
                                         + ", with light " + l, truck.canPass(t, l));
                        }
                    }
                } 
            }
        }
    }

    /**
     * Test method for {@link Truck#chooseDirection(java.util.Map)}.
     */
    @Test
    public void testChooseDirection() {
        // There is an assumption that there will always be at least one valid choice
        // for the chooseDirection() method to return. No test for surrounded by WALLs!
        
        // Trucks need to stay on their own terrain
        // (STREET and LIGHT are considered the same Terrain for this purpose)
        // Trucks choose randomly from among directions which lead to STREET or LIGHT
        
        // If a Truck starts on STREET it should also be willing to move to LIGHT
        // If a Truck starts on LIGHT it should also be willing to move to STREET
        
        // The program should not freeze
        // if a Truck is on STREET and the only valid choices are LIGHT
        // if a Truck is on LIGHT and the only valid choices are STREET

        final Map<Direction, Terrain> neighbors = new HashMap<Direction, Terrain>();


        for (final Terrain t : Terrain.values()) {
            
            neighbors.put(Direction.WEST, Terrain.WALL);
            neighbors.put(Direction.NORTH, Terrain.WALL);
            /*   W
             * W ? ?
             *   ?
             */
            if (t == Terrain.WALL || t == Terrain.GRASS || t == Terrain.TRAIL) {
                continue; // Trucks don't start on WALLs, Grass, or Trails.
            }
            final Truck truck = new Truck(0, 0, Direction.NORTH);
            
            neighbors.put(Direction.EAST, t);

            // provide both STREET and LIGHT options
            if (t == Terrain.STREET) {
                neighbors.put(Direction.SOUTH, Terrain.LIGHT);
            } else {
                neighbors.put(Direction.SOUTH, Terrain.STREET);
            } 
            

            /*   W
             * W t t
             *   ?         LIGHT, STREET, or t depending on t
             */
            int tries = 0;
            boolean seenWest = false;
            boolean seenEast = false;
            while (tries < TRIES_FOR_RANDOMNESS) {
                tries = tries + 1;
                final Direction dir = truck.chooseDirection(neighbors);

                assertSame(dir, Direction.EAST);                   
                    
                seenEast = seenEast || dir == Direction.EAST;
            }

            assertTrue("truck randomness", seenEast);
            
            // now check with only one valid option    
            neighbors.put(Direction.EAST, Terrain.WALL);
            /*   W
             * W t W
             *   ?         LIGHT, STREET, or t depending on t
             */

            tries = 0;
            while (tries < TRIES_FOR_RANDOMNESS) {
                tries = tries + 1;
                final Direction dir = truck.chooseDirection(neighbors);
                assertSame("invalid dir chosen, should be south, was " + dir,
                           Direction.SOUTH, dir);
            }
            
            // Check for dead right or left
            neighbors.put(Direction.WEST, Terrain.STREET);
            neighbors.put(Direction.EAST, Terrain.LIGHT);
            
            //System.out.println(neighbors.toString());
            tries = 0;
            seenWest = false;
            seenEast = false;
            System.out.println(neighbors.toString());
            while (tries < TRIES_FOR_RANDOMNESS) {
                tries = tries +1;
                final Direction dir = truck.chooseDirection(neighbors);
                assertTrue("on " + t + ", should choose east or west, was " + dir,
                           dir == Direction.EAST || dir == Direction.WEST);
                seenWest = seenWest || dir == Direction.WEST;
                seenEast = seenEast || dir == Direction.EAST;
            }
            
            assertTrue("truck randomness issue! WEST : " + seenWest
                       + "; EAST : " + seenEast, seenWest && seenEast);

        }
    }

}
