
SRCS := State.sml EParser.sml ELexer.sml ESyntax.sml Extended.sml Core.sml # StateSet.sml
OBJS := $(SRCS:.sml=.ui) $(SRCS:.sml=.uo)

ISRCS := ESyntax.sml Core.sml E2C.sml Interpreter.sml
IOBJS := $(ISRCS:.sml=.ui) $(IRSC:.sml=.uo)

all : Extended Interpreter

Interpreter: $(IOBJS)
	mosmlc -o Interpreter Interpreter.sml

E2C: $(IOBJS) 
	mosmlc -o E2c E2C.sml

Extended : $(OBJS)
	mosmlc -c Extended.sml

ELexer.sml : ELexer.lex ESyntax.sml 
	mosmllex ELexer.lex

ESyntax.sml : Core.ui E2C.ui

EParser.sml EParser.sig : EParser.grm ESyntax.sml
	mosmlyac -v EParser.grm

ELexer.uo : EParser.sig
ELexer.ui : ELexer.sml EParser.uo
	mosmlc -c ELexer.sml

%.uo %.ui : %.sml 
	mosmlc -c -I $(MUDDYHOME) $*.sml

EParser.ui : EParser.sig
	mosmlc -c $^

EParser.uo : EParser.sml
	mosmlc -c EParser.sml

EParser.ui : ESyntax.ui

State.ui : 
	mosmlc -c State.sml

Core.ui :   State.ui ESyntax.ui
	mosmlc -c  Core.sml

ESyntax.ui :   State.ui
	mosmlc -c ESyntax.sml

E2C.ui : State.uo Core.ui E2C.sml
	mosmlc -c   E2C.sml

# StateIntInt.ui : State.ui
# 	mosmlc -c -toplevel  StateIntInt.sml

SharedNodeStateSet.ui : E2C.ui

# StateStringString.ui : State.ui
# 	mosmlc -c -toplevel  StateStringString.sml

# StateStringStringSplay.ui : State.uo
# 	mosmlc -c -toplevel  StateStringStringSplay.sml
# State.ui :
# 	mosmlc -c State.sig

# StateIntInt.ui :
# 	mosmlc -c StateIntInt.sml


# StateIntInt.ui :
# 	mosmlc -c StateIntInt.sml


#StateSte.ui : StateSet.sml
#State.uo : State.sig
#	mosmlc -c State.sig

clean:
	rm -f *.ui *.uo EParser.sig EParser.sml ELexer.sml Extended Interpreter



