package edu.nyu.pqs.stopwatch.impl;

import java.lang.System;

/**
 * Lap class which are stored as objects of a Stopwatch object
 * @author nicolelee
 *
 */
public class Lap {
	private long startTime;
	private long lastEndTime;
	private long duration;
	private boolean running;

	public Lap() {
		this.startTime = System.currentTimeMillis();
		this.lastEndTime = System.currentTimeMillis();
		this.duration = 0;
		this.running = true;
	}
	
	/**
	 * Setter for lastEndTime
	 */
	public void setLastEndTime() {
		this.lastEndTime = System.currentTimeMillis();
	}
	
	/**
	 * Updates the duration of this lap
	 * @param currentTime
	 */
	public void updateTime() {
		long timeToAdd = System.currentTimeMillis() - this.lastEndTime;
		this.duration += timeToAdd;
	}
	
	/**
	 * Getter for this lap's duration
	 * @return long, the current time held by the lap
	 */
	public long getDuration() {
		return duration;
	}

	/**
	 * returns a boolean to represent if this is the current lap 
	 * of the stopwatch
	 * @return boolean, true if running, false if not
	 */
	public boolean isRunning() {
		return this.running;
	}
	
	/**
	 *  terminates the lap
	 */
	public void end() {
		this.running = false;
	}

	/**
	 * @return if the object equals this lap
	 * true if it equals
	 * false if it does not equal
	 * based on the startTime
	 */
	@Override
	public boolean equals(Object o) {
		if (!(o instanceof Lap)) {
			return false;
		}
		Lap lapToCheck = (Lap) o;
		if (this == lapToCheck) {
			return true;
		}
		else {
			return ((this.startTime == lapToCheck.startTime));
		}	
	}
	
	/**
	 * @return The hash code of this Lap
	 */
	@Override
	public int hashCode() {
		int result = 17;
		return result * 31 + (int)(this.startTime ^ (this.startTime >>> 32));
	}

	/**
	 * @return The string of this lap
	 */
	@Override
	public String toString() {
		String str = "[Lap: lastEndTime=" + this.lastEndTime;
		str += ", duration=" + this.duration;
		str += ", isRunning=" + (this.running ? "true" : "false");
		str += " ]";
		return str;
	}
}
