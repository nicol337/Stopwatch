package edu.nyu.pqs.stopwatch.impl;

import edu.nyu.pqs.stopwatch.api.IStopwatch;
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

/**
*
* One implementation of a thread-safe object that can be used for timing laps.  
* Stopwatch objects are created in the StopwatchFactory.  Different threads 
* can share a single stopwatch object and safely call any of the stopwatch 
* methods.
* @author nicolelee (nkl223@nyu.edu)
*/
public class Stopwatch implements IStopwatch{
	private String id;
	private boolean running;
	private List<Lap> lapList;
		
	/**
	 * Public initializer for Stopwatch
	 * @param id necessary for Stopwatch
	 */
	public Stopwatch(String id) {
		this.id = id;
		this.running = false;
		this.lapList = new CopyOnWriteArrayList<Lap>();
	}
	
	/**
	 * Public getter for the id
	 * @return the Id of this stopwatch.  Will never be empty or null.
	 */
	@Override
	public String getId() {
		return this.id;
	}

	/**
	 * Starts the stopwatch. Creates a new lap if this is the first time the stopwatch
	 * is started. Resumes current lap if there is already a running lap.
	 * @throws IllegalStateException if called when the stopwatch is already running
	 */
	@Override
	public void start() {
		if (this.running) {
			throw new IllegalStateException("Stopwatch " + this.id + " is already running");
		}
		this.running = true;
		if(this.lapList.isEmpty()) {
			Lap newLap = new Lap();
			this.lapList.add(newLap);
		}
		else {
			Lap currentLap = this.getCurrentLap();
			if (!currentLap.isRunning()) {
				Lap newLap = new Lap();
				this.lapList.add(newLap);
			}
			else {
				currentLap.setLastEndTime();
			}
		}
	}
		
	/**
	 * Stores the time elapsed since the last time lap() was called
	 * or since start() was called if this is the first lap.
	 * @throws IllegalStateException if called when the stopwatch isn't running
	 */
	@Override
	public void lap() {
		if (!this.running) {
			throw new IllegalStateException("Stopwatch " + this.id + " is not running");
		}
		Lap currentLap = this.getCurrentLap();
		currentLap.updateTime();
		currentLap.end();
		Lap newLap = new Lap();
		this.lapList.add(newLap);
	}

	/**
	 * Stops the stopwatch (and records one final lap).
	 * @throws IllegalStateException if called when the stopwatch isn't running
	 */
	@Override
	public void stop() {
		if (!this.running) {
			throw new IllegalStateException("Stopwatch " + this.id + " is not running");
		}	
		this.running = false;
		Lap currentLap = this.getCurrentLap();
		currentLap.updateTime();
	}
	
	/**
	 * A private, thread-safe method to deterministically get the current lap
	 * @return Lap that is the current running lap of the stopwatch
	 */
	private Lap getCurrentLap() {
		if(this.lapList.isEmpty()) {
			throw new NullPointerException("Laplist is empty");
		}
		else {
			Iterator<Lap> lapListIterator = lapList.listIterator(lapList.size()-1);
			Lap currentLap = lapListIterator.next();
			return currentLap;
		}
	}

	/**
	 * Resets the stopwatch.  If the stopwatch is running, this method stops the
	 * watch and resets it.  This also clears all recorded laps.
	 */
	@Override
	public void reset() {
		this.stop();
		Iterator<Lap> lapListIterator = this.lapList.iterator();
		while (lapListIterator.hasNext()) {
			lapListIterator.next();
			lapListIterator.remove();
		}
	}

	/**
	 * Returns a list of lap times (in milliseconds).  This method can be called at
	 * any time and will not throw an exception.
	 * @return a list of recorded lap times or an empty list if no times are recorded.
	 */
	@Override
	public List<Long> getLapTimes() {
		List<Long> lapTimes = new ArrayList<Long>();
		Iterator<Lap> lapListIterator = lapList.iterator();
		while (lapListIterator.hasNext()) {
			lapTimes.add(lapListIterator.next().getDuration());
		}
		return lapTimes;	
	}
	
	/**
	 * @return boolean, true if o equals this Stopwatch
	 * false if o does not
	 */
	@Override
	public boolean equals(Object o) {
		if (!(o instanceof Stopwatch)) {
			return false;
		}
		Stopwatch other = (Stopwatch) o;
		if (this == other) {
			return true;
		}
		return this.id.equals(other.id);
	}
	
	/**
	 * @return The hash code of this Stopwatch
	 */
	@Override
	public int hashCode() {
		int result = 17;
		return result * 31 + this.id.hashCode();
	}
	
	/**
	 * @return String representing this Stopwatch
	 */
	@Override
	public String toString() {
		String str = "[Stopwatch id: " + this.id + ": ";
		str += ", running=" + (this.running ? "true" : "false");
		str += ", lapList={";
		Iterator<Lap> iterator = lapList.iterator();
		while (iterator.hasNext()) {
			str+=iterator.next().toString();
		}
		str += " }]";
		return str;
	}
}
