
import java.*;
import java.io.*;
import java.util.*;
import java.util.regex.*;
import java.lang.*;

class Scanner {
    public static Vector Num_tok= new Vector(5,2);
    public static Enumeration Num_Enum = Num_tok.elements();
    public static Vector Word_tok= new Vector(5,2);
    public static Enumeration Word_Enum = Word_tok.elements();
    public static Vector Op_tok= new Vector(5,2);
    public static Enumeration Op_Enum = Op_tok.elements();       
    public static String NUMBER_TOKEN = "toknumber";
    public static String WORD_TOKEN = "tokword";
    public static String OPERATOR_TOKEN = "tokop";               
           
    
    
    
   public void getTokens(String tokens)                              //this function breaks string in tokens
    {
        StringTokenizer newtokens = new StringTokenizer(tokens);
        while (newtokens.hasMoreTokens())				//checks if another token is available
			{                            
            String token = newtokens.nextToken() ;
            String tokenType = getTokenType(token) ;
           System.out.println(token + "\t\t" + tokenType);           //the type of token is returned
	            
        }

    }
    

   

    
    private String getTokenType(String token) {
        if(token != null) {
            if (Pattern.matches("[\\d]+", token)) {                 //checks if it is a number token
                return NUMBER_TOKEN;
          } else if (Pattern.matches("[\\w]+", token)) {           //checks if it is a word token
                return WORD_TOKEN;
            } else {
                return OPERATOR_TOKEN;                             // return value operator token
            }
        }
        return null;
    }


    public static void main(String s[]) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));     //create Buffered reader using system.in to read       
        int i, strlen;
        Vector vtok = new Vector(5, 2);
        Enumeration vEnum = vtok.elements();
        String getinput,getinput1;                                                  // to get input string from user and store it                 
        Scanner sc = new Scanner();

        System.out.println("Start typing your code and when you finish write EXIT: ");
        
        do {
            getinput = br.readLine();
			if (getinput.endsWith("exit"))
				   {
					   strlen = getinput.length();
			           strlen -= 4;
					   getinput = getinput.substring(0,strlen);         
                       getinput1 = ("exit");                            // so that as soon as exit is typed in the end 
					   vtok.addElement(new String(getinput));           
					   vtok.addElement(new String(getinput1));
                       break;
				   }
			else vtok.addElement(new String(getinput));
           } 
		while (!getinput.equalsIgnoreCase("exit"));


        getinput = "";

        while (!getinput.equalsIgnoreCase("exit"))
 {
            while (vEnum.hasMoreElements()) {

				getinput = (String) vEnum.nextElement();
                if (getinput.endsWith("exit"))
				   {
					   strlen = getinput.length();
			           strlen -= 4;
					   getinput1 = getinput.substring(0,strlen);        
                       sc.getTokens(getinput1);
                       break;
                   }
				else
                    sc.getTokens(getinput);                  // call to function getToken() to identify tokens
            }

        }
    }
}
