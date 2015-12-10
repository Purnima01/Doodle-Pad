package edu.nyu.model;
import java.awt.event.MouseEvent;
import java.util.HashSet;
import java.util.Set;

import edu.nyu.views.IListener;

public class Model {
  private static Model instance;
  private int numListeners;
  
  private Model() {
    numListeners = 0;
  }
  
  /**Get singleton instance of model*/
  public static Model getInstance() {
    if (instance == null) {
      instance = new Model();
    }
    return instance;
  }
  
  Set<IListener> listeners = new HashSet<IListener>();
  
  /**Registers a new listener. Duplicate registration of 
   *listeners is not allowed.
   *@return -1 if this method fails for some reason
   *        monotonically increasing ID otherwise.
   */
  public int registerListener(IListener newListener) {
    if (newListener == null) {
      throw new NullPointerException();
    }
    if (listeners.contains(newListener)) {
      return -1;
    }
    
    listeners.add(newListener);
    numListeners ++;
    return numListeners;
  }
  
  /**Listener calls this when the mouse button has just been pressed*/
  public void getMouseClickedPoint(MouseEvent e) {
    for (IListener canvas : listeners) {
      canvas.notifyMovePoints(e.getPoint());
    }
  }
  
  /**Listener informs the model when mouse is pressed and dragged on screen*/
  public void getMouseDragged(MouseEvent e) {
    for (IListener canvas : listeners) {
      canvas.notifyMovePoints(e.getPoint());
    }
  }

  /**Remove listener if listener no longer wants to receive updates*/
  public void removeListener(IListener listener) {
    listeners.remove(listener);
  }
  
  /**Get the current number of listeners registered with the model*/
  public int numberOfListenersRegistered() {
    return listeners.size();
  }
  
  /**Start a new drag next time the user presses the mouse*/
  public void mouseReleased() {
    for (IListener canvas : listeners) {
      canvas.notifyMouseRelease();
    }
  }

  /**Used by the listener when user wishes to clear the screen*/
  public void informClearScreen() {
    for (IListener canvas : listeners) {
      canvas.clearScreen();
    }
  }
  
  /**For testing only*/
  public void setInstanceOfModelToNull() {
    instance = null;
  }

}
