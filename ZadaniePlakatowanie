package Plakatowanie;

import java.io.*;
import java.nio.file.*;
import java.time.*;
import java.util.*;

public class ZadaniePlakatowanie {

	public static void main(String[] args) {
		
		Instant poczatek = Instant.now();
		
		List<String> wymiaryBudynkow = pobierzWymiaryZPliku();
		
		if (wymiaryBudynkow != null)
		{
			int liczbaPlakatow = obliczLiczbePlakatow(wymiaryBudynkow);	
		    zapiszWynikDoPliku(liczbaPlakatow);
		}
		
		Instant koniec = Instant.now();
		System.out.println("Czas wykonania: " + Duration.between(poczatek, koniec).toMillis() + " milisekund");
		
	}
	
	public static List<String> pobierzWymiaryZPliku()
	{
		List<String> wymiaryBudynkow = null;
		
		Path path = Paths.get("pla.in");
		
		try 
		{
			wymiaryBudynkow = Files.readAllLines(path);
		} 
		catch (IOException e) 
		{
			System.out.println("Problem z wczytaniem pliku: " + e);
			return null;
		}
		
		if (wymiaryBudynkow.size() > 0)
			wymiaryBudynkow.remove(0);
		
		return wymiaryBudynkow;
	}
	
	public static int obliczLiczbePlakatow(List<String> wymiaryBudynkow)
	{
		int liczbaPlakatow = 0;
		
		Deque<Integer> stosWysokosci = new ArrayDeque<>();
		
		int poprzedniaWysokosc = 0;
		int biezacaWysokosc = 0;
		
		for(String wymiaryLinia: wymiaryBudynkow)
		{
			String[] wymiary = wymiaryLinia.split(" ");
			biezacaWysokosc = Integer.parseInt(wymiary[1]);
			
			if (biezacaWysokosc > poprzedniaWysokosc)
			{
				liczbaPlakatow++;
				stosWysokosci.push(poprzedniaWysokosc);
				poprzedniaWysokosc = biezacaWysokosc;
			}
			else if (biezacaWysokosc < poprzedniaWysokosc)
			{
				while (stosWysokosci.peek()>biezacaWysokosc) stosWysokosci.poll();

				poprzedniaWysokosc = biezacaWysokosc;
					
				if (stosWysokosci.peek()<biezacaWysokosc)	
					liczbaPlakatow++;
				else stosWysokosci.poll();
				
			}
		}
		
		return liczbaPlakatow;
	}
	
	public static void zapiszWynikDoPliku(int liczbaPlakatow){
		
		Path pathOut = Paths.get("pla.out");
		
		try (BufferedWriter writer = Files.newBufferedWriter(pathOut)) 
		{
			writer.write(String.valueOf(liczbaPlakatow));
		} 
		catch (IOException e) 
		{
			System.out.println("Problem z zapisem pliku: " + e);
		}
	}
}
