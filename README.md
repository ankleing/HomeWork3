# HomeWork3
## 项目1
![image1](https://github.com/ankleing/HomeWork3/tree/main/image/image1) 
```
  protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        requestWindowFeature(Window.FEATURE_NO_TITLE);
        setContentView(R.layout.activity_main);
        /**创建列表获得名字和图片 */
        List<Map<String,Object>> ListItems=new ArrayList<Map<String, Object>>();
        for (int i=0;i<names.length;i++){
            Map<String,Object> listItem=new HashMap<String,Object>();
            listItem.put("header",names[i]);
            listItem.put("images",image[i]);
            ListItems.add(listItem);
        }
        /**包装成SimpAdpter*/
        SimpleAdapter simpleAdapter=new SimpleAdapter(this,ListItems,R.layout.simple_items,new String[]{"header","images"},new int[]{R.id.header,R.id.images});
        final ListView list=findViewById(R.id.MyList);
        list.setAdapter(simpleAdapter);
        /**点击后弹出对应的名字*/
        list.setOnItemClickListener(new AdapterView.OnItemClickListener(){
            public void onItemClick(AdapterView<?> parent, View view, int position, long id){
                        view.setSelected(true);
                        CharSequence text=names[position];
                        Toast .makeText(MainActivity.this,text,Toast.LENGTH_SHORT).show();
            }
        });
    }
```
## 项目2
![image2](https://github.com/ankleing/HomeWork3/tree/main/image/image2) 
```
  public void onClick(View view) {
        customDialog();
    }
    public void customDialog(){
        AlertDialog.Builder builder = new AlertDialog.Builder(MainActivity2.this);
        final AlertDialog dialog =builder.create();
        /** 使当前页面点击按钮弹出dialog*/
        View dialogView =View.inflate(MainActivity2.this,R.layout.dialog,null);
        dialog.setView(dialogView);
        dialog.show();

    }
```
## 项目3
![image3](https://github.com/ankleing/HomeWork3/tree/main/image/image3) 
```
  public boolean onCreateOptionsMenu(Menu menu) {
        /** 创建菜单*/
        MenuInflater inflater = getMenuInflater();
        inflater.inflate(R.menu.menu, menu);
        return true;
    }
    /** 设置选项的效果*/
    public boolean onOptionsItemSelected(MenuItem item){
        switch (item.getItemId()){
            case R.id.submenu_item1:
                txt.setTextSize(10);break;
            case R.id.submenu_item2:
                txt.setTextSize(16);break;
            case R.id.submenu_item3:
                txt.setTextSize(20);break;
            case R.id.item1:
                Toast.makeText(this,item.getTitle(),Toast.LENGTH_SHORT).show();break;
            case R.id.submenu_item4:
                txt.setTextColor(Color.RED);break;
            case R.id.submenu_item5:
                txt.setTextColor(Color.BLACK);break;
        }
        return true;
    }
```
## 项目4
![image4](https://github.com/ankleing/HomeWork3/tree/main/image/image4) 
```
       /**自定义适配器的getView */
    public View getView(final int position, View convertView, ViewGroup parent) {

        final ViewHolder viewHolder;
        if(convertView==null){
            /**加载名字和图片*/
            convertView=View.inflate(context, R.layout.activity_data, null);
            viewHolder=new ViewHolder();
            viewHolder.textView=convertView.findViewById(R.id.str);
            viewHolder.imageView=convertView.findViewById(R.id.im);
            convertView.setTag(viewHolder);
        }else{
            viewHolder=(ViewHolder) convertView.getTag();
        }
        int green = Color.parseColor("#FF4081");
        int white = Color.parseColor("#ffffff");
        viewHolder.textView.setText(list.get(position).getName());
        viewHolder.imageView.setImageResource(R.drawable.robot);
        /** 被选择就改变颜色 */
        if(list.get(position).isBo()){
            viewHolder.textView.setBackgroundColor(green);
        }
        else {
            viewHolder.textView.setBackgroundColor(white);
        }
        return convertView;

    }
```
  
```
  public void onItemCheckedStateChanged(ActionMode mode, int position, long id, boolean checked) {

               /**实时刷新标志位，并计算选择的项目数 */
                if (checked) {
                    list.get(position).setBo(true);
                    adapter.notifyDataSetChanged();
                    num++;
                } else {
                    list.get(position).setBo(false);
                    adapter.notifyDataSetChanged();
                    num--;
                }
                mode.setTitle("  " + num + " Selected");
            }
```
