Java

	//  binary: 1111 1111 1111 0001
	int hexValue = 0xFFF1;
	
	short value = (short)(hexValue);
	// value = -15 

to ActionScript

	//  binary: 1111 1111 1111 0001
	var hexValue:int = 0xFFF1;
	
	// get everything except the signed bit "111 1111 1111 0001"
	var unsignedValue:Number = (hexValue & 0x7FFF);  
	// unsignedValue now equals 32,753
	
	var signedValue:Number = unsignedValue;
	
	// if the signed flag is set, flip the value
	if ((hexValue >> 15) == 1) {
	    signedValue = unsignedValue - 0x8000;   // 0x800 =  32,768 (maximum 15 bit number)
	}
	
	// signedValue = -15
