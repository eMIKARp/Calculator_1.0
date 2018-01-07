# Calculator_1.0
a simple application which helps to add, substract, divide and multiply any nubmers 
    
    package calculator;

    /**
     * Import paczek zawierających klasy wykorzystywane w dalszej cześci programu
     */

    import javax.swing.*;
    import java.awt.*;
    import java.awt.event.*;


    public class Main extends JFrame {
    
    /**
     * Definiowanie zmiennych używanych w dalszej cześci programu
     */
    

    JPanel panelOutput = new JPanel();
    JPanel panelInput = new JPanel();
    JTextArea outputArea = new JTextArea(6,30);
    
    Double argDzialania[] = new Double[2];
    Double wynDzialania[] = new Double[1];
    
    boolean flagaPierwszegoDzialania = false;
    boolean flagaCzyPoprzedniZnakToLiczba = false;
    boolean flagaCzyPoprzedniZnakToRownaSie = false;
    
    String opDzialania = "";
    char kZnak; 
    
    /**
    * Konstruktor klasy głównej aplikacji
    */
    
    public Main()
    {
        initComponents();
    }

    /**
    * Wywołanie głównej metody w aplikacji 
    */
    
    public static void main(String[] args) 
    {
        new Main();
    }
    
    /**
    * Metoda odpowiedzialna za inicializacje komponentów zawartych w oknie aplikacji 
    */
    
    public void initComponents()
    {
        /**
        * Rysowanie okna głównego aplikacji wraz z nadawaniem mu podstawowych własności
        */
        
        this.setTitle("Kalkulator by Emil Karpowicz");
        this.setBounds(300,300,360,200);
        // oknoGlowne.pack();
        //oknoGlowne.setLocationRelativeTo(null);
        this.setResizable(false);
        this.setDefaultCloseOperation(JFrame.DISPOSE_ON_CLOSE);
        this.setVisible(true);
        
        /**
        * Zdefinowanie zarządcy rozkładu dla poszczególnych kontenerów
        */
        
        this.setLayout(new GridLayout(2,1,1,1));
        panelOutput.setLayout(new BorderLayout());
        panelInput.setLayout(new GridLayout(4,4,1,1));
        
        /**
        * Dodanie komponentów do poszczególnych kontenerów
        */
        
        this.getContentPane().add(panelOutput);
        this.getContentPane().add(panelInput);
        
        panelOutput.add(outputArea);
    
        outputArea.setFont(new Font("Arial", Font.BOLD,18));
               
        zbudujButtonNum("6");
        zbudujButtonNum("7");
        zbudujButtonNum("8");
        zbudujButtonNum("9");
        zbudujButtonNum("4");
        zbudujButtonNum("5");  
        zbudujButtonNum("+");
        zbudujButtonNum("-");
        zbudujButtonNum("2");
        zbudujButtonNum("3");
        zbudujButtonNum("*");
        zbudujButtonNum("/");
        zbudujButtonNum("0");
        zbudujButtonNum("1");
        zbudujButtonNum("=");
        zbudujButtonNum("del");
          
        
    }
    
    public void zbudujButtonNum(String nazwa)
    {
        JButton nowyButton = new JButton(nazwa);
        panelInput.add(nowyButton);

        nowyButton.addActionListener(new ActionListener() 
        {
            
            @Override
            public void actionPerformed(ActionEvent e) 
            {        
                kZnak = ((JButton)e.getSource()).getText().charAt(0);
                        
                if (kZnak >= '0' && kZnak <= '9')
                    {   
                        if (flagaCzyPoprzedniZnakToLiczba == false || flagaCzyPoprzedniZnakToRownaSie == true)  outputArea.setText(null);
                        if (opDzialania == "/" && kZnak == '0')
                        {
                            outputArea.setText("Nie dziel przez zero!");
                            flagaCzyPoprzedniZnakToLiczba = false;
                        
                        }
                        else
                        {    
                        if (outputArea.getText().equals("") && kZnak == '0' && flagaPierwszegoDzialania == false)
                            {
                                outputArea.setText(null);
                            }
                         else
                            {
                                outputArea.append(((JButton)e.getSource()).getText());
                                flagaCzyPoprzedniZnakToLiczba = true;

                            }
                        }
                        
                    }    

                else if (nowyButton.getText() == "del")
                    {
                        outputArea.setText(null);
                        argDzialania[0] = 0.0;
                        argDzialania[1] = 0.0;
                        wynDzialania[0] = 0.0;
                        flagaPierwszegoDzialania = false;
                        flagaCzyPoprzedniZnakToLiczba = false;
                    
                    }
                else if (kZnak == '+')
                    {
                        if (flagaCzyPoprzedniZnakToLiczba == true) 
                            {
                            opDzialania = ((JButton)e.getSource()).getText();
                            argDzialania[1] = Double.parseDouble(outputArea.getText());
                            if (flagaPierwszegoDzialania == true) 
                                wynDzialania[0] = argDzialania[1] + argDzialania[0]; 
                            else 
                                wynDzialania[0] = argDzialania[1];
                            System.out.println(wynDzialania[0]);
                            argDzialania[0] = wynDzialania[0];
                            flagaPierwszegoDzialania = true;
                            flagaCzyPoprzedniZnakToLiczba = false;
                            outputArea.setText(null);
                            }
                        else
                            {
                            outputArea.setText("Wprowadź argumenty do działania!");
                            }
                    }
                
                else if (kZnak == '-')
                    {
                        if (flagaCzyPoprzedniZnakToLiczba == true) 
                            {
                            opDzialania = ((JButton)e.getSource()).getText();
                            argDzialania[1] = Double.parseDouble(outputArea.getText());
                            if (flagaPierwszegoDzialania == true) 
                                wynDzialania[0] = argDzialania[1] - argDzialania[0]; 
                            else 
                                wynDzialania[0] = argDzialania[1];
                            System.out.println(wynDzialania[0]);
                            argDzialania[0] = wynDzialania[0];
                            flagaPierwszegoDzialania = true;
                            flagaCzyPoprzedniZnakToLiczba = false;
                            outputArea.setText(null);
                            }
                        else
                            {
                            outputArea.setText("Wprowadź argumenty do działania!");
                            }
                    }
                
                else if (kZnak == '*')
                    {
                    if (flagaCzyPoprzedniZnakToLiczba == true) 
                        {
                        opDzialania = ((JButton)e.getSource()).getText();
                        argDzialania[1] = Double.parseDouble(outputArea.getText());
                        if (flagaPierwszegoDzialania == true) 
                            wynDzialania[0] = argDzialania[1] * argDzialania[0]; 
                        else 
                            wynDzialania[0] = argDzialania[1];
                        System.out.println(wynDzialania[0]);
                        argDzialania[0] = wynDzialania[0];
                        flagaPierwszegoDzialania = true;
                        flagaCzyPoprzedniZnakToLiczba = false;
                        outputArea.setText(null);
                        }
                    else
                        {
                        outputArea.setText("Wprowadź argumenty do działania!");
                        }
                    }
                
                 else if (kZnak == '/')
                    {
                    if (flagaCzyPoprzedniZnakToLiczba == true) 
                        {
                        opDzialania = ((JButton)e.getSource()).getText();
                        argDzialania[1] = Double.parseDouble(outputArea.getText());
                        if (flagaPierwszegoDzialania == true)
                            wynDzialania[0] = argDzialania[1] / argDzialania[0]; 
                        else 
                            wynDzialania[0] = argDzialania[1];
                        System.out.println(wynDzialania[0]);
                        argDzialania[0] = wynDzialania[0];
                        flagaPierwszegoDzialania = true;
                        flagaCzyPoprzedniZnakToLiczba = false;
                        outputArea.setText(null);
                        }
                    else
                        {
                        outputArea.setText("Wprowadź argumenty do działania!");
                        }
                    }
               
                else if (nowyButton.getText() == "=")
                    {
                    if (flagaCzyPoprzedniZnakToLiczba == true) 
                        {
                        System.out.println(opDzialania);
         
                        if (opDzialania == "+") wynDzialania[0] = wynDzialania[0] + Double.parseDouble(outputArea.getText());
                        else if (opDzialania == "-") wynDzialania[0] = wynDzialania[0] - Double.parseDouble(outputArea.getText());
                        else if (opDzialania == "*") wynDzialania[0] = wynDzialania[0] * Double.parseDouble(outputArea.getText());
                        else if (opDzialania == "/") wynDzialania[0] = wynDzialania[0] / Double.parseDouble(outputArea.getText());
                        else wynDzialania[0] = wynDzialania[0];
                                                
                        System.out.println(wynDzialania[0]);
                        outputArea.setText(null);
                        outputArea.setText((wynDzialania[0].toString()));
                        argDzialania[0] = 0.0;
                        argDzialania[1] = 0.0;
                        wynDzialania[0] = 0.0;
                        opDzialania= ((JButton)e.getSource()).getText();
                        
                        flagaPierwszegoDzialania = false;
                        flagaCzyPoprzedniZnakToRownaSie = true;
                        }
                    else
                        {
                        outputArea.setText("Wprowadź argumenty do działania!");
                        }
                        
                                
                    }
            }    
          
        });
    }
    
}
