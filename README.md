# slip11


Q.1 Write a java program to implement Adapter pattern to design Heart Model to Beat

Q2. Write a python program to find all null values in a given dataset and remove them.

Q3. Create a node.js file that Select all records from the "customers" table, and delete the
specified record.


Q.1 Write a java program to implement Adapter pattern to design Heart Model to Beat
Model

:

interface BeatModelInterface {
void initialize();
void on();
void off();
void setBPM(int bpm); 
int getBPM();
void registerObserver(BeatObserver o);
void removeObserver(BeatObserver o);
void registerObserver(BPMObserver o);
void removeObserver(BPMObserver o);
}
 class BeatModel implements BeatModelInterface, MetaEventListener {
Sequencer sequencer;
ArrayList beatObservers = new ArrayList();
ArrayList bpmObservers = new ArrayList();
int bpm = 90;
// other instance variables here
public void initialize() {
setUpMidi();
buildTrackAndStart();
}
public void on() {
sequencer.start();
setBPM(90);
}
public void off() {
setBPM(0);
sequencer.stop();
}
public void setBPM(int bpm) {
this.bpm = bpm;
sequencer.setTempoInBPM(getBPM());
notifyBPMObservers();
}
public int getBPM() {
return bpm;
}
void beatEvent() {
notifyBeatObservers();
}
// Code to register and notify observers
// Lots of MIDI code to handle the beat
}
 class DJView implements ActionListener, BeatObserver, BPMObserver {
BeatModelInterface model;
ControllerInterface controller;
JFrame viewFrame;
JPanel viewPanel;
BeatBar beatBar;
JLabel bpmOutputLabel;
public DJView(ControllerInterface controller, BeatModelInterface model) {
this.controller = controller;
this.model = model;
model.registerObserver((BeatObserver)this);
model.registerObserver((BPMObserver)this); 
}
public void createView() {
// Create all Swing components here
}
public void updateBPM() {
int bpm = model.getBPM();
if (bpm == 0) {
bpmOutputLabel.setText("offline");
} else {
bpmOutputLabel.setText("Current BPM: " + model.getBPM());
}
}
public void updateBeat() {
beatBar.setValue(100);
}
}
 interface ControllerInterface {
void start();
void stop();
void increaseBPM();
void decreaseBPM();
void setBPM(int bpm);
}
 class BeatController implements ControllerInterface {
BeatModelInterface model;
DJView view;
public BeatController(BeatModelInterface model) {
this.model = model;
view = new DJView(this, model);
view.createView();
view.createControls();
view.disableStopMenuItem();
view.enableStartMenuItem();
model.initialize();
}
public void start() {
model.on();
view.disableStartMenuItem();
view.enableStopMenuItem();
}
public void stop() {
model.off();
view.disableStopMenuItem();
view.enableStartMenuItem();
}
public void increaseBPM() {
int bpm = model.getBPM();
model.setBPM(bpm + 1); 
}
public void decreaseBPM() {
int bpm = model.getBPM();
model.setBPM(bpm - 1);
}
public void setBPM(int bpm) {
model.setBPM(bpm);
}
}
public class Main {
public static void main (String[] args) {
BeatModelInterface model = new BeatModel();
ControllerInterface controller = new BeatController(model);
}
}


Q2. Write a python program to find all null values in a given dataset and remove them.
:-
df = df.dropna(how='any',axis=0) 


#Recreate random DataFrame with Nan values
df = pd.DataFrame(index = pd.date_range('2017-01-01', '2017-01-10', freq='1d'))
# Average speed in miles per hour
df['A'] = np.random.randint(low=198, high=205, size=len(df.index))
df['B'] = np.random.random(size=len(df.index))*2

#Create dummy NaN value on 2 cells
df.iloc[2,1]=None
df.iloc[5,0]=None

print(df)
                A         B
2017-01-01  203.0  1.175224
2017-01-02  199.0  1.338474
2017-01-03  198.0       NaN
2017-01-04  198.0  0.652318
2017-01-05  199.0  1.577577
2017-01-06    NaN  0.234882
2017-01-07  203.0  1.732908
2017-01-08  204.0  1.473146
2017-01-09  198.0  1.109261
2017-01-10  202.0  1.745309

#Delete row with dummy value
df = df.dropna(how='any',axis=0)

print(df)

                A         B
2017-01-01  203.0  1.175224
2017-01-02  199.0  1.338474
2017-01-04  198.0  0.652318
2017-01-05  199.0  1.577577
2017-01-07  203.0  1.732908
2017-01-08  204.0  1.473146
2017-01-09  198.0  1.109261
2017-01-10  202.0  1.745309


df = df.dropna(how='any',axis=0) 


#Recreate random DataFrame with Nan values
df = pd.DataFrame(index = pd.date_range('2017-01-01', '2017-01-10', freq='1d'))
# Average speed in miles per hour
df['A'] = np.random.randint(low=198, high=205, size=len(df.index))
df['B'] = np.random.random(size=len(df.index))*2

#Create dummy NaN value on 2 cells
df.iloc[2,1]=None
df.iloc[5,0]=None

print(df)
                A         B
2017-01-01  203.0  1.175224
2017-01-02  199.0  1.338474
2017-01-03  198.0       NaN
2017-01-04  198.0  0.652318
2017-01-05  199.0  1.577577
2017-01-06    NaN  0.234882
2017-01-07  203.0  1.732908
2017-01-08  204.0  1.473146
2017-01-09  198.0  1.109261
2017-01-10  202.0  1.745309

#Delete row with dummy value
df = df.dropna(how='any',axis=0)

print(df)

                A         B
2017-01-01  203.0  1.175224
2017-01-02  199.0  1.338474
2017-01-04  198.0  0.652318
2017-01-05  199.0  1.577577
2017-01-07  203.0  1.732908
2017-01-08  204.0  1.473146
2017-01-09  198.0  1.109261
2017-01-10  202.0  1.745309



Q3)Create a node.js file that Select all records from the "customers" table, and delete the
specified record
:

var mysql = require('mysql');
var con = mysql.createConnection({
 host: "localhost",
user: "yourusername",
 password: "yourpassword",
database: "mydb"
});
con.connect(function(err) {
 if (err) throw err;
 var sql = "DELETE FROM customers WHERE address = 'Mountain 21'";
 con.query(sql, function (err, result) {
 if (err) throw err;
 console.log("Number of records deleted: " + result.affectedRows);
});
});
