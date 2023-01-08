# GuessNumber
用verilog在FPGA上實作猜數字遊戲




module test(input[0:3]IN,
				input load1,load2,load3,load4,
				input compare,
				input CLK,reset,
				output reg[0:3] Anode_Activate,
				output reg[0:6]LED_out);
	wire[0:1]LED_Activating_Counter;
	reg [0:32]fresh_Counter;
	reg [0:3]LED_BCD;
	reg [0:3]IN_A;
	reg [0:3]IN_B;
	reg [0:3]IN_C;
	reg [0:3]IN_D;
	
	divfreq F0(CLK,CLK_div);
	

	
	always@(posedge CLK_div or posedge reset) 
	begin
		if(reset)
		begin
			fresh_Counter <= 0;
			
		end
		else
			fresh_Counter <= fresh_Counter + 1;
	end
	assign LED_Activating_Counter = fresh_Counter[30:31];
	
	always@*
	begin
		if(load1==1 && LED_Activating_Counter==2'b00)
		begin
			Anode_Activate <= 4'b0111;
			IN_A <= IN;
			LED_BCD <= IN_A;
		end
		else if(load2==1 && LED_Activating_Counter==2'b01)
		begin
			Anode_Activate <= 4'b1011;
			IN_B <= IN;
			LED_BCD <= IN_B;
		end
		else if(load3==1 && LED_Activating_Counter==2'b10)
		begin
			Anode_Activate <= 4'b1101;
			IN_C <= IN;
			LED_BCD <= IN_B;
		end
		else if(load4==1 && LED_Activating_Counter==2'b11)
		begin
			Anode_Activate <= 4'b1110;
			IN_D <= IN;
			LED_BCD <= IN_A;
	
		end
		else
			case(LED_Activating_Counter)
				2'b00:begin Anode_Activate <= 4'b0111;	LED_BCD <= IN_A;end
				2'b01:begin Anode_Activate <= 4'b1011;	LED_BCD <= IN_B;end
				2'b10:begin Anode_Activate <= 4'b1101;	LED_BCD <= IN_C;end
				2'b11:begin Anode_Activate <= 4'b1110;	LED_BCD <= IN_D;end
			endcase
	end
	
	always @(LED_BCD)
	begin
		case(LED_BCD)
			4'b0000: LED_out = 7'b0000001; // "0"     
			4'b0001: LED_out = 7'b1001111; // "1" 
			4'b0010: LED_out = 7'b0010010; // "2" 
			4'b0011: LED_out = 7'b0000110; // "3" 
			4'b0100: LED_out = 7'b1001100; // "4" 
			4'b0101: LED_out = 7'b0100100; // "5" 
			4'b0110: LED_out = 7'b0100000; // "6" 
			4'b0111: LED_out = 7'b0001111; // "7" 
			4'b1000: LED_out = 7'b0000000; // "8"     
			4'b1001: LED_out = 7'b0000100; // "9" 
			default: LED_out = 7'b0000001; // "0"
		endcase
	end
endmodule


module divfreq(input CLK, output reg CLK_div);
	reg [24:0] Count = 25'b0;
	always @(posedge CLK)
		begin
			if(Count > 10000)
				begin
					Count <= 25'b0;
					CLK_div <= ~CLK_div;
				end
			else
				Count <= Count + 1'b1;
		end
endmodule
