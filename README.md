## Grafana-Prometheus-Dashboard

A1.Install [Prometheus](https://prometheus.io/download/) according to OS
2.Extract from win and open folder 
3.Navigate to directory like
      
    C:\Users\LDIN\Downloads\prometheus-3.2.1.windows-amd64\prometheus-3.2.1.windows-amd64>
    
4.Now open cmd and add This command that starts the Prometheus server using the specified configuration file
[WINDOWS]

    prometheus.exe --config.file=prometheus.yml

Will be met with 

    ![image](https://github.com/user-attachments/assets/dda883bb-4100-45a8-a954-b43982f68422)

Prometheus is now be accessible at [http://localhost:9090](http://localhost:9090)

A2.Download [Grafana](https://grafana.com/grafana/download)

Change Drive if needed, continue with default values on dashboard 

Navigate to folder 
    
    cd D:\Grafana\bin
    
Start Grafana

    grafana-server.exe

Access Grafana

Open your browser and go to [http://localhost:3000](http://localhost:3000)
Default login:
Username: admin
Password: admin (change when you will be asked to)

![image](https://github.com/user-attachments/assets/18b35015-2aed-4d6a-86a6-c0207a826ae4)


A3.The Prometheus Node Exporter is primarily designed for Unix-based systems and doesn't support Windows natively. 
However, for Windows environments, there's an equivalent tool called the Windows Exporter
(formerly known as wmi_exporter). 
This exporter collects Windows system metrics and exposes them for Prometheus to scrape.

[Windows Exporter GitHub Releases page.](https://github.com/prometheus-community/windows_exporter/releases)

1.Download Latest .msi installer and run it,keep below fields as they are 

![image](https://github.com/user-attachments/assets/4b6b681a-c3b5-46de-8bcd-8c29176a3b48)

By default, the exporter listens on port 9182

2.Open a web browser and navigate to [http://localhost:9182/metrics]([http://localhost:9182/metrics)

![image](https://github.com/user-attachments/assets/610d367f-a815-4523-90d7-9ba9d3b44601)

3.Configure Prometheus to Scrape Metrics:

Open prometheus.yml config file 

Add a new job under the scrape_configs section to instruct 
Prometheus to scrape metrics from the Windows Exporter:

    scrape_configs:
      - job_name: 'windows_exporter'
        static_configs:
          - targets: ['localhost:9182']


Restart Prometheus by navigating to ist folder ,type cmd above and with cmd :-

    prometheus.exe --config.file=prometheus.yml


Collect Grafana to Prometheus

1.Navigate to Prometheus folder and run prometheus according to above instructions 
2. Check if prometheus is running
  open [http://localhost:9090](http://localhost:9090) in your browser.
  Go to Status → Targets and ensure localhost:9182 (Windows Exporter) is UP.

  ![image](https://github.com/user-attachments/assets/88e27d4b-7351-4941-bec8-558e5e9d5e51)

  click Target Health

  ![image](https://github.com/user-attachments/assets/4046cce7-88da-4c38-a2fb-0cec283a3ac4)

Step 3: Add Prometheus as a Data Source in Grafana

Open Grafana → Go to http://localhost:3000

Login (admin / admin) and change your password if prompted.

Click on Home -> Connections -> Data sources 

![image](https://github.com/user-attachments/assets/6124c3bd-661e-4cf3-ba4b-9c875c93967b)

Select Add Data Source 

![image](https://github.com/user-attachments/assets/4507ba22-f08f-486a-8c58-b08e9ae6eb1c)

Select Prometheus 

Set the URL to

    http://localhost:9090

![image](https://github.com/user-attachments/assets/4bc18bfc-77f9-44cf-93de-306597315427)

Click "Save & Test".

If successful, it will say "Data source is working!" ✅

![image](https://github.com/user-attachments/assets/ab2cc729-7cce-40b9-aa90-22cc9c63023b)

Visualize Metrics IN Grafana 

Import a pre-built dashboard tailored for the Windows Exporter:​

Navigate to the [Windows Node Exporter dashboard on Grafana Labs](https://grafana.com/grafana/dashboards/14499-windows-node/).

Note the dashboard ID 14499 .

In Grafana, click on the + icon and select Import.

Enter the dashboard ID and proceed to load the dashboard.

Select your Prometheus data source and import the dashboard.

This dashboard provides visualizations for various Windows system metrics,

including CPU usage, memory utilization, disk activity, and network statistics.












  

  




