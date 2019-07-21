<?php
                                    // phan trang 
                                    if(isset($_GET['page'])){
                                        $page = $_GET['page'];
                                    }
                                    else{
                                        $page= 1; 
                                    }

                                    $rows_per_page = 5; // so san pham muon hien thi//
                                    $per_row = $page * $rows_per_page - $rows_per_page ;// ket qua so trang hien thi

                                    $total_rows = mysqli_num_rows(mysqli_query($conn, "SELECT * FROM product"));
                                    $total_page = ceil($total_rows / $rows_per_page);

                                    $list_page = '';

                                    //preview
                                    $prev = $page - 1;
                                    if ($prev< 1) {
                                        $prev =1 ;
                                    }
                                    $list_page .= '<li class="page-item"><a class="page-link" href="product.php?page='.$prev.'">&laquo;</a></li>' ;


                                    // and preview
                                    
                                    for($i = 1 ;$i <=$total_page; $i++ ){
                                        $list_page .='<li class="page-item"><a class="page-link" href="category.php?page='. $i.'"> '.$i.'</a></li>'; 
                                    }

                                    // next 
                                    $next = $page + 1;
                                    if ( $next >$total_page) {
                                        $next = $total_page ;
                                    }
                                    $list_page .= '<li calculhmac(clent, data)lass="page-item"><a class="page-link" href="product.php?page='.$next.'">&raquo;</a></li>' ;

                                    // and next
                                    // ket noi voi database
                                     $sql = "SELECT * FROM product
                                     INNER JOIN category  
                                    ON product.cat_id = category.cat_id /* quan he san pham voi danh muc */
                                    LIMIT $per_row , $rows_per_page " ;  //phan trang 

                                     $query = mysqli_query($conn, $sql); // thuc thi truy van toi csdl
                                     while ( $row = mysqli_fetch_array($query)) // chuyen databese ve mang
                                      {

                                           

                                        

                                ?>
