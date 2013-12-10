**********************
Data types of Domogik
**********************

||__Created:__|xx/xx/2011
__Creator:__|Ferllings
__Reviewers:__|
__Status:__|{GAUGE(value=>40, max=>100, label=>''review'', perc=>true, labelsize=>50, height=>20, color=>green, bgcolor=>#EEEEEE)}{GAUGE}
__Target:__|0.3.0
__References:__|((Database_core_model|Database Model))||

Boolean type
=============

__Feature options for Boolean__:(none)

*DT_Trigger (0,1=Trigger)
*DT_Bool (0=False, 1=True)
**DT_Switch (0=Off, 1=On)
**DT_Enable (0=Disable, 1=Enable)
**DT_Binary (0=Low, 1=High)
**DT_Step (0=Decrease, 1=Increase)
**DT_UpDown (0=Up, 1=Down)
**DT_OpenClose (0=Open, 1=Close)
**DT_Start (0=Stop, 1=Start)
**DT_State (0=Inactive, 1=Active)

Number type (float or integer)
===============================

__Feature options for Number:__
*Min value
*Max value
*Unit symbol

*DT_Number
**DT_Scaling (range=0,100; unit=%)
**DT_Angle (range=0,360; unit=°)
**DT_Brightness (unit=lux)
**DT_Temp (unit=°C)
**DT_TempK (unit=K)
**DT_TempF (unit=°F)
**DT_Pression (unit=Pa)
**DT_Humidity (unit=%)
**DT_AirQuality (unit=ppm)
**DT_Volt (unit=V)
**DT_mVolt (unit=mV)
**DT_kVolt (unit=kV)
**DT_Current (unit=A)
**DT_mCurrent (unit=mA)
**DT_kCurrent (unit=kA)
**DT_Power (unit=W)
**DT_mPower (unit=mW)
**DT_kPower (unit=kW)
**DT_ActiveEnergy (unit=Wh)
**DT_mActiveEnergy (unit=mWh)
**DT_kActiveEnergy (unit=kWh)
**DT_ApparantEnergy (unit=VAh)
**DT_Speed (unit=m/s)
**DT_kmhSpeed (unit=km/h)
**DT_Year (unit=Year; integer only)
**DT_Month (range=1,12; unit=Month; integer only)
**DT_Day (range=1,31; unit=Day; integer only)
**DT_Hour (range=0,23; unit=h; integer only)
**DT_Minute (range=0,59; unit=min; integer only)
**DT_Second (range=0,59; unit=s; integer only)
**DT_mSecond (range=0,999; unit=ms; integer only)
**DT_Timestamp (integer only)

String type
============

__Feature options for String:__
*Max length

*DT_Char (ASCII 0,127)
*DT_String
**DT_Phone (format= international (ex. +33122334455))
**DT_Hexa
***DT_ColorRGBHexa (format Hexadecimal = RRGGBB, length = 6)

Set type
=========

*DT_DayOfWeek (range=0,7)
**1=Monday
**2=Tuesday
**3=Wednesday
**4=Thursday
**5=Friday
**6=Saturday
**7=Sunday
**0=no day
*DT_HVACHeat (range=0,4)
**0=Auto
**1=Comfort
**2=Standby
**3=Economy
**4=Building Protection
*DT_HVACVent (range=0,4)
**0=Auto
**1=Heat
**2=Cool
**3=Fan only
**4=Dry
*DT_ColorCII (range= Colour Index International)
**W=White
**O=Orange
**R=Red
**Y=Yellow
**B=Blue
**G=Green
**Bk=Black
**Br=Brown

Date/Time type
===============

*DT_DateTime (format ISO=YYYY-MM-DDThh:mm:ss.s)
**DT_Date (format ISO=YYYY-MM-DD)
**DT_Time (format ISO=hh:mm:ss.s)

List type
==========

Comma separated values
*DT_List
**DT_ColorRGB (format = (R 0-255),(G 0-255),(B 0-255) (ex. '10,145,230'))
**DT_ColorCMYK (format = (C 0-100%),(M 0-100%),(Y 0-100%),(K 0-100%) (ex. '10,90,33,50'))
