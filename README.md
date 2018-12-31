# Weather-Station
//A weather station measures temperature and pressure and has a list of subscribed weather observers. When there is an update on the measures, the weather station publishes the update to all currently-subscribed observers. 
import java.util.ArrayList;
import java.util.List;

public class WeatherStation {

	private List<WeatherObserver> theSubscribed;
	private double temp, prSig;

	/**
	 * Initialize a new weather station.
	 * 
	 * @param t initial temperature measure
	 * @param p initial pressure measure
	 */
	public WeatherStation(double t, double p) {
		
		this.temp = t;
		this.prSig = p;
		this.theSubscribed = new ArrayList<>();
	}

	/**
	 * Subscribe the input weather observer o as one of the observers of the current
	 * weather station. Add the input o to the list of subscribed observers.
	 * 
	 * @param o a weather observer
	 */
	public void subscribe(WeatherObserver o) {
		
		if (o != null) {
			o.setWeatherStation(this);
			this.theSubscribed.add(o);
		}
	}

	/**
	 * Unsubscribe the input weather observer o from the list of observers of the
	 * current weather station. Remove the input o from the list of subscribed
	 * observers. Assume that the input o is an already-subscribed observer.
	 * 
	 * @param o a weather observer
	 */
	public void unsubscribe(WeatherObserver o) {
				o.setWeatherStation(null);
		this.theSubscribed.remove(o);
	}

	/**
	 * Publish the latest readings of weather data to all subscribed observers. That
	 * is, perform an update on each subscribed observer.
	 */
	public void publish() {
		
		for (WeatherObserver w : this.theSubscribed) {
			w.update();
		}
	}

	/**
	 * Get the list of subscribed weather observers.
	 * 
	 * @return an array of subscribed weather observers.
	 */
	public WeatherObserver[] getObservers() {
		
		WeatherObserver[] arra = new WeatherObserver[this.theSubscribed.size()];
		if (this.theSubscribed.size() > 0) {
			this.theSubscribed.toArray(arra);
		}
		return arra;
	}

	/**
	 * Get the latest temperature measure.
	 * 
	 * @return latest temperature measure
	 */
	public double getTemperature() {
		
		return this.temp;
	}

	/**
	 * Get the latest pressure measure.
	 * 
	 * @return latest pressure measure
	 */
	public double getPressure() {
		
		return this.prSig;
	}

	/**
	 * Update the weather data
	 * 
	 * @param t new temperature measure
	 * @param p new pressure measure
	 */
	public void set_measurements(double t, double p) {
		
		this.temp = t;
		this.prSig = p;
	}
}
