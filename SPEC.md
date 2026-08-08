MUMPS (IRIS)

Goal: Create a web based Instrument Interface Dashboard

This thing should cycle thru a lit of interfaces (see ^Instruments below) and 
display each on a row on the screen. The fields will be the name of the interface/instrument,
a button for control purposes.

Button Text:
STATUS		Button Text	Button Status
=============================================
STARTING	STARTING	Disabled	
RUNNING		STOP		Enabled
STOPPING	STOPPING	Disabled
STOPPED		START		Enabled

Finally, a button to view the log for a given interface. From that screen the user
can view the log, clear it, etc.

Global ^Instruments

^Instruments(UNIT_NUM) = INSTRUMENT_NAME | STATUS
^Instruments(UNIT_NUM, "CONTROL") = START_RTN | STOP_RTN
^Instruments(UNIT_NUM, "ERRORS", ERROR_IDX) = DATE_OF_ERROR
^Instruments(UNIT_NUM, "ERRORS", ERROR_IDX, "ERRORTEXT", TEXT_IDX) = ERROR_TEXT
^Instruments(UNIT_NUM, "LOGGING", LOG_IDX) = LOG_DATE
^Instruments(UNIT_NUM, "LOGGING", LOG_IDX, TEXT_IDX) = LOG_TEXT

UNIT_NUM	Unique internal unit number (1-nnn)
INSTRUMENT_NAME	The name of the interface/instrument
STATUS		STARTING, RUNNING, STOPPING, STOPPED
START_RTN	MUMPS Starting routine
STOP_RTN	MUMPS Stopping routine
ERROR_IDX	Internal error number 1-nnn
DATE_OF_ERROR	DAte error occurred
ERROR_TEXT	Cause of error, stack, anything else.
TEXT_IDX	Internal text index number, 1-nnn
LOG_IDX		Internal log index, 1-nnn
LOG_TEXT	Log verbiage


Example Acquisition START routine:
START(IDX,INSTRUMENT_NAME) {
	S ^Instruments(IDX) = INSTRUMENT_NAME | "STARTING";
	...
	...go thru start up, serial, etc.
	...
	....
	S ^Instruments(IDX) = INSTRUMENT_NAME | "RUNNING"
}
