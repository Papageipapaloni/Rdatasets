.. container::

   ===== ===============
   ozone R Documentation
   ===== ===============

   .. rubric:: Monthly ozone measurements over Central America.
      :name: monthly-ozone-measurements-over-central-america.

   .. rubric:: Description
      :name: description

   This data set is a subset of the data from the 2006 ASA Data expo
   challenge, http://stat-computing.org/dataexpo/2006/. The data are
   monthly ozone averages on a very coarse 24 by 24 grid covering
   Central America, from Jan 1995 to Dec 2000. The data is stored in a
   3d area with the first two dimensions representing latitude and
   longitude, and the third representing time.

   .. rubric:: Usage
      :name: usage

   ::

      ozone

   .. rubric:: Format
      :name: format

   A 24 x 24 x 72 numeric array

   .. rubric:: References
      :name: references

   http://stat-computing.org/dataexpo/2006/

   .. rubric:: Examples
      :name: examples

   ::

      value <- ozone[1, 1, ]
      time <- 1:72
      month.abbr <- c("Jan", "Feb", "Mar", "Apr", "May",
       "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
      month <- factor(rep(month.abbr, length = 72), levels = month.abbr)
      year <- rep(1:6, each = 12)
      deseasf <- function(value) lm(value ~ month - 1)

      models <- alply(ozone, 1:2, deseasf)
      coefs <- laply(models, coef)
      dimnames(coefs)[[3]] <- month.abbr
      names(dimnames(coefs))[3] <- "month"

      deseas <- laply(models, resid)
      dimnames(deseas)[[3]] <- 1:72
      names(dimnames(deseas))[3] <- "time"

      dim(coefs)
      dim(deseas)
