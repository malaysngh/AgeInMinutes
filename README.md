# AgeInMinutes
import android.app.DatePickerDialog
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button
import android.widget.TextView
import android.widget.Toast
import java.text.SimpleDateFormat
import java.util.*

class MainActivity : AppCompatActivity() {
   private var selectedDate:TextView?=null
   private var minutesOfAge: TextView?= null
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)


         minutesOfAge = findViewById(R.id.tv2)
        selectedDate =findViewById(R.id.tv1)
        val myButton: Button = findViewById(R.id.myButton)

        myButton.setOnClickListener {
           clickDatePicker()


        }
    }
    private fun clickDatePicker(){
        val myCalendar= Calendar.getInstance()
        val year = myCalendar.get(Calendar.YEAR)
        val month =myCalendar.get(Calendar.MONTH)
        val day=myCalendar.get(Calendar.DAY_OF_MONTH)
        val dpd = DatePickerDialog(this,
        {_, selectedYear , selectedMonth , dayOfMonth->
            Toast.makeText(this , "Year : $selectedYear, Month: ${selectedMonth+1},Day of Month: $dayOfMonth", Toast.LENGTH_SHORT).show()
        val selectedDate2= "$dayOfMonth/${selectedMonth+1}/$selectedYear"
            selectedDate?.text = selectedDate2
            val sdf =SimpleDateFormat("dd/MM/yyyy" ,Locale.ENGLISH)
            val theDate = sdf.parse(selectedDate2)
            theDate?.let {   val selectedDateInMinutes=theDate.time/60000
                val currentDate=sdf.parse(sdf.format(System.currentTimeMillis()))
                currentDate?.let { val currentDateInMinutes = currentDate.time/60000
                    val difference = currentDateInMinutes-selectedDateInMinutes
                    minutesOfAge?.text=difference.toString() } }
        }, year, month, day)
        dpd.datePicker.maxDate = System.currentTimeMillis()-86400000
        dpd.show()


    }
}
