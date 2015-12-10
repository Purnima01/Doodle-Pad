package edu.nyu.views;

import java.awt.BorderLayout;
import java.awt.Cursor;
import java.awt.Dimension;
import java.awt.Graphics;
import java.awt.Image;
import java.awt.Point;
import java.awt.Toolkit;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.event.MouseMotionListener;
import java.util.ArrayList;
import java.util.List;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;

import edu.nyu.model.Model;

/**Listener class that registers with the model*/
public class Canvas implements IListener{
  private Model model;
  private List<Point> points = new ArrayList<Point>();
  private List<List<Point>> history = new ArrayList<List<Point>>();
  private JFrame frame;
  private GUI gui;
  private Image image;
  private JButton clearScreen;
  
  /**Registers with the model on creation*/
  public Canvas(Model theModel) {
    if (theModel == null) {
      throw new NullPointerException();
    }
    this.model = theModel;
    model.registerListener(this);
    frame = new JFrame();
    gui = new GUI();
    frame.add(gui);
    frame.setSize(500, 500);
    frame.setVisible(true);
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
  }
  
  private class GUI extends JPanel implements MouseListener, MouseMotionListener {

    GUI() {
      setPreferredSize(new Dimension(1280, 700));
      addMouseListener(this);
      addMouseMotionListener(this);
      setClearScreenButton();
    }
    
    private void setClearScreenButton() {
      clearScreen = new JButton("Clear screen");
      clearScreen.setCursor(new Cursor(Cursor.HAND_CURSOR));
      add(clearScreen, BorderLayout.SOUTH);
      
      clearScreen.addActionListener(new ActionListener() {

        @Override

        public void actionPerformed(ActionEvent arg0) {
          model.informClearScreen();
        }

      });
    }
    
    private void clearScreen() {
      history.clear();
      points.clear();
      repaint();
    }

    private void notifyMovePoints(Point p) {
      points.add(p);
      repaint();
    }

    @Override
    public void mouseClicked(MouseEvent e) {}

    @Override
    public void mouseDragged(MouseEvent e) {
      //inform model
      model.getMouseDragged(e);
    }

    private void setCursorForFrame() {
      Toolkit toolkit = Toolkit.getDefaultToolkit();
      image = toolkit.getImage(getClass().getResource("/images/pencil.png"));
      Cursor cursor = toolkit.createCustomCursor(image,new Point(0,17), "pencil");
      frame.setCursor(cursor);
    }

    protected void paintComponent(Graphics g) {
      super.paintComponent(g);
      setCursorForFrame();
      
      //print points from previous drags
      for (List<Point> prv : history) {
        for (int i = 0; i < prv.size() - 1; i++) {
          Point p1 = prv.get(i);
          Point p2 = prv.get(i + 1);
          g.drawLine(p1.x, p1.y, p2.x, p2.y);
        }
      }
      
      //print points in current drag
      for (int i = 0; i < points.size() - 1; i++) {
        Point p1 = points.get(i);
        Point p2 = points.get(i + 1);
        g.drawLine(p1.x, p1.y, p2.x, p2.y);
      }
    }

    @Override
    public void mouseMoved(MouseEvent e) {}

    @Override
    public void mousePressed(MouseEvent e) {}

    @Override
    public void mouseReleased(MouseEvent e) {
      model.mouseReleased();
    }
    
    @Override
    public void mouseEntered(MouseEvent e) {}

    @Override
    public void mouseExited(MouseEvent e) {}
  }

  @Override
  public void notifyMovePoints(Point p) {
    gui.notifyMovePoints(p);
  }

  @Override
  public void notifyMouseRelease() {
    List<Point> pointsInThisDrag = new ArrayList<Point>();
    pointsInThisDrag.addAll(points);
    history.add(pointsInThisDrag);
    points.clear(); 
  }
  
  /**Clear the screen completely*/
  public void clearScreen() {
    gui.clearScreen();
  }

}
