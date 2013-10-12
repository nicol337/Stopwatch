package edu.nyu.pqs.stopwatch.impl;

import java.util.Iterator;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;
import edu.nyu.pqs.stopwatch.api.IStopwatch;

/**
 * The StopwatchFactory is a thread-safe factory class for IStopwatch objects.
 * It maintains references to all created IStopwatch objects and provides a
 * convenient method for getting a list of those objects.
 * @author nicolelee (nkl223@nyu.edu)
 *
 */
public class StopwatchFactory {
	private static StopwatchFactory INSTANCE = null;
	private static List<IStopwatch> stopwatchList;
	
	/**
	 * private constructor of StopwatchFactory
	 */
	private StopwatchFactory() {
		stopwatchList = new CopyOnWriteArrayList<IStopwatch>();
	}
	
	/**
	 * To enforce the singleton property of the StopwatchFactory
	 * @return StopwatchFactory The only instance of the factory
	 */
	public static StopwatchFactory getInstance() {
		if (INSTANCE == null) {
			INSTANCE = new StopwatchFactory();
		}
		return INSTANCE;
	}
	
	/**
	 * Creates and returns a new IStopwatch object
	 * @param id The identifier of the new object
	 * @return The new IStopwatch object
	 * @throws IllegalArgumentException if <code>id</code> is empty, null, or already
   *     taken.
	 */
	public static IStopwatch getStopwatch(String id) {
		getInstance();
		if (!isIdValid(id)) {
			throw new IllegalArgumentException(id + " is empty, null, "
							+ "or is already taken");
		}
		Stopwatch stopwatch = new Stopwatch(id);
		stopwatchList.add(stopwatch);
		return stopwatch;	
	}
	
	/**
	 * A validation method to check of the id string is non-empty, non-null,
	 * and not already taken
	 * @param id
	 * @return boolean if the id is a valid id
	 */
	private static boolean isIdValid(String id) {
		 if (id == null || id.equals("") || foundStopWatch(id)) {
			 return false;
		 }
		 return true;
	}

	/**
	 * A validation submethod to check if the id string is already taken
	 * @param id
	 * @return boolean true if the id is found in the Stopwatch list
	 */
	private static boolean foundStopWatch(String id) {
		Iterator<IStopwatch> stopwatchListIterator = getStopwatches().iterator();
		while (stopwatchListIterator.hasNext()) {
			if (stopwatchListIterator.next().getId().equals(id)) {
				return true;
			}
		}
		return false;
	}

	/**
	 * Returns a list of all created stopwatches
	 * @return a List of al creates IStopwatch objects.  Returns an empty
	 * list if no IStopwatches have been created.
	 */
	public static List<IStopwatch> getStopwatches() {
		getInstance();
		List<IStopwatch> stopwatches = new ArrayList<IStopwatch>();
		if (stopwatchList.isEmpty()) {
			return stopwatches;
		}
		Iterator<IStopwatch> stopwatchListIterator = stopwatchList.iterator();
		while (stopwatchListIterator.hasNext()) {
			stopwatches.add(stopwatchListIterator.next());
		}
		return stopwatches;	
	}
}
