dwca-importer
=============

Shell scripts that downloads a DWC-Archive given an url, unzip, parses and converts to a csv format and sends the data to DataBase

If you are using it with a java application, you just need to put the files at "jboss/bin" and to call the script via code.

E.g.:
	
import java.io.BufferedReader;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStreamReader;

public class DWCAClass
{
	public String executeDWCAImporter(String processType, String source) throws IOException, FileNotFoundException, Exception  
	{
	    final File batchFile = new File("script_dwca.sh");// jboss/bin/
	
	    final ProcessBuilder processBuilder = new ProcessBuilder(batchFile.getAbsolutePath(), processType, source);
	    processBuilder.redirectErrorStream(true);
	    //processBuilder.redirectOutput(outputFile);
	    final Process process = processBuilder.start();
	    final int exitStatus = process.waitFor();
	    
	}
}

And you just call:
public static void main (String args[])
{
	DWCA dwcaImporter = new DWCA();
	//if you want to pass a xls or xlsx file you must pass "0" argument and the name of file
	dwcaImporter.executeDWCAImporter("0","dwcaarchive.xls");
	//if you want to pass a url you must pass "1" argument and the link, in zip or xls or xlsx format
	dwcaImporter.executeDWCAImporter("1","http://urltodwcaarchive");
}


=============
ISSUES
=============
If your xls/xlsx file have a sheet name different for Plan1, you must to change the Sheet name to Plan1 or update script to read the sheet name given, in line 64, change Plan1 for YourSheetName:
perl excel2csv.pl -e $DEST/$pathDWCA/planilha_dwca"$1" -s Plan1 > $DEST/$pathDWCA/occurrence.txt 
